# Principles and Guidelines for Metrics Design

This document covers some of our general guidelines that we use when designing
metrics. 

This document covers only the principles for quantitative metrics covered under
'Productivity' in [Developer Productivity and Happiness: Goals &
Signals](dph-goals-and-signals.md).

These principles are not about the operational metrics of various tools and
services. "Operational metrics" are the ones that a team owning a tool uses to
understand if it's currently working, how it's broken, its current performance,
etc. Think of Operational metrics as something you would use in monitoring and
alerting of a production service.

This doc also doesn't cover the business metrics for tools—the ones that measure
their business goals/success—like how many users they have.

There might be some overlap of operational, business, and productivity metrics,
though. That is, some productivity metrics might also be business metrics, and a
very few of them could also be used as operational metrics.

- [Measuring Results vs. Measuring Work](#measuring-results-vs-measuring-work)
- [Time Series](#time-series)
  - [Exclude Weekends](#exclude-weekends)
  - [Defined Weeks](#defined-weeks)
  - [Timestamps](#timestamps)
  - [Use the End Time, not the Start Time](#use-the-end-time-not-the-start-time)
- [Developers vs. Machines](#developers-vs-machines)
- [Common Dimensions](#common-dimensions)
- [Going Up or Down Must Be Meaningful](#going-up-or-down-must-be-meaningful)
  - [Prefer Graphs That Are Good When They Go Up](#prefer-graphs-that-are-good-when-they-go-up)
- [Retention](#retention)
- [Business Hours](#business-hours)
  - [Fallback System](#fallback-system)

## Measuring Results vs. Measuring Work

We want to measure the impact, results, or effects of our work, rather than just
measuring how much work gets done. Otherwise, our metrics just tell us we're
doing work—they don't tell us if we're doing the _right_ work.

As an analogy, let's say we owned a packing plant (like, a place where they put
things in boxes) and we're installing new conveyor belts on the assembly line.
We could measure the progress of installing the belts (i.e., "how many belts
have been fully installed?") or we could measure the _effect_ of the belts on
the quantity and quality of our packing ("how many boxes get packed?" and "what
percentage of boxes pass quality inspection?"). We would rather measure the
latter. 

## Time Series

Unless stated otherwise, all of our metrics are a time series. That is, they are
plotted on a graph against time—we count them per day or per week as
appropriate. Most commonly, we count them per week, as that eliminates
confusions around weekends and minor fluctuations between days. In particular,
with some metrics, Mondays and Fridays tend to have lower or higher values than
other days, and aggregating the data over a week eliminates those fluctuations.

### Exclude Weekends

If you show daily graphs, you should exclude weekends from all metrics unless
they seem very relevant for your particular metric. We exclude weekends because
they make the graphs very hard to read. (We don't exclude holidays—those are
_usually_ understandable anomalies that we actually _want_ to be able to see in
our graphs. Also, not all offices have the same holidays.) You can include
weekends in all other types of graphs other than daily graphs. 

### Defined Weeks

Unless you have good reason for another requirement, weeks should be measured
from **12:00am Friday to the end of Thursday**. Cutting off our metrics at the
end of Thursday gives executives enough time to do reviews and investigations
for Monday or Tuesday meetings. When we cannot specify a time zone, we should
assume we are measuring things in the `America/Los_Angeles` time zone. However,
all data should be _stored_ in the **UTC** time zone.

### Timestamps

All times should be stored ideally as microseconds, but if that's not possible,
then as milliseconds. As engineering systems grow, there can be more and more
events that happen _very_ close in time, but which we need to put in order for
certain metrics to work. (For example, a metric might need to know when each
test in a test suite ended, and if all the tests are running in parallel, these
end times could be very close together.)

### Use the End Time, not the Start Time

When you display a metric on a graph, the event you are measuring should be
assigned to a date or time on the graph by the _end time_ of the event. For
example, let's imagine we have a daily graph that shows how long our CI jobs
take. If a CI job takes two days to finish, it should show up on the graph on
the day that it _finished_, not the day that it started.

This prevents having to "go back in time" and update previous data points on the
graph in a confusing way. (This is especially bad if it changes whether the
graph is going up or going down multiple days _after_ a manager has already
looked at the graph and made plans based on its trend.)

## Developers vs. Machines

Almost all our productivity metrics are defined by saying "a developer" does
something. **For each metric,** we need to have two different versions of the
same metric: one for when machines do the task, and one for when people do the
task. For example, we need to measure human beings doing `git clone` and
the CI system (or any other automated system) doing `git clone` separately.

**The most important metrics are the ones where people do the task, not the ones
where machines do the task.** But we still need to be able to measure the
machines doing the task, as that is sometimes relevant for answering questions
about developer productivity.

Sometimes, a question comes up on whether to count something as being machine
time or developer time. For example, let's say a developer types a command on
their machine that causes the CI system to run a bunch of tests. The question to
ask is, "Most of the time, is this action costing us developer time?" A
developer doesn't have to just be sitting there and waiting for the action to
finish, for it to be costing us developer time. Maybe it takes so long that they
switch contexts, go read email, go eat lunch, etc. That's still developer cost.
On the other hand, let's say there is a daily automated process that runs a test
and then reports the test result to a developer. We would count the time spent
running that test as "machine time," because it wasn't actively spending
developer time.

This is particularly relevant when looking at things that happen in parallel.
When we measure "developer time" for parallel actions, we only care about how
much wall-clock time was taken up by the action, not the sum total of machine
hours used to execute it. For example, if I run 10 tests in parallel that each
take 10 minutes, I only spent 10 minutes of developer time, even though I spent
100 minutes of machine time.

## Common Dimensions

There are a few common dimensions that we have found useful for slicing most of
our metrics:

1. By Team (i.e., the team that the affected developer is on)
2. By code repository (or codebase, when considering a large repo)
3. By location the developer sits in

Most metrics should also support being sliced by the above dimensions. There are
many other dimensions that we slice metrics by, some of which are special to
each metric; these are just the _common_ dimensions we have found to be the most
useful.

## Going Up or Down Must Be Meaningful

It should be clearly good or bad when a metric goes up, and clearly good or bad
when it goes down. One direction should be good, and the other direction should
be bad.

This should not change at a certain threshold. For example, let’s say you have a
metric that’s "bad" when it goes down until it’s at 90%, and then above 90% it’s
either meaningless or it’s actually good when it goes down (like you want it
always to be at 90%). 

Consider redesigning such metrics so that they are always good when they go up
and always bad when they go down. For example, in the case of the metric that’s
supposed to always be at 90%, perhaps measure how far away teams are from being
at 90%.

### Prefer Graphs That Are Good When They Go Up

We should strive to make metrics that are "good" when they go up and "bad" when
they go down. This makes it consistent to read graphs, which makes life easier
for executives and other people looking at dashboards. This isn't always
possible, but when we have the choice, this is the way we should make the
choice.

## Retention

Prefer to retain data about developer productivity metrics forever. Each of
these metrics could potentially need to be analyzed several years back into the
past, especially when questions come up about how we have affected productivity
over the long term. The actual cost to LinkedIn of storing these forever is
_extremely_ small, whereas the potential benefit to the business from being able
to do long-term analysis is huge.

Of course, if there are legitimate legal or regulatory constrains on retention,
make sure to follow those. However, there are rarely such constraints on the type
of data we want to retain.

## Business Hours

Some metrics are defined in terms of "business hours."

Basically, we are measuring the _perceived_ wait time experienced by a
developer. For example, imagine Alice sends off a code review request at 5pm
and then goes home. Bob, in another time zone, reviews that code while Alice is
sleeping. Alice comes back into work the next day and experiences a code review
that, for her, she received in zero hours.

The ideal way to measure business hours would be to do an automated analysis for
each individual to determine what their normal working hours are (making sure to
keep this information confidential, only use it as an input to our productivity
metrics, and never expose it outside of our team). Once you have established
this baseline for each individual (which you will have to update on some regular
basis) you only count time spent by individuals during those hours.

For any calendar day in the developer's local time zone, do not count more than
8 hours a day. It is confusing to have "business days" that are longer than 8
hours. So if a task takes two days to complete, and a developer was somehow
working on it full time for each day, it would show up as 16 business hours
(even if they worked 9 hours each day). This helps normalize out the differences
in schedules between engineers. (For some metrics we may need to relax this
restriction---we would determine that on a case-by-base basis when we develop
the metric.)

The reason that we are picking 8 hours is that what we care the most about here
is the cost to the company, and even though most software engineers are
salaried, we are measuring their cost to the company in 8-hour-a-day increments.
It would be unusual for any salaried engineer anywhere in the world to have
_contractual obligations_ to work more than 8 hours a day.

### Fallback System

If you cannot generate an automated analysis of working hours for each
individual, then set the "business day" as being 7am to 7pm in their local time
zone. We don't use 9am to 5pm because the schedule of developers varies, and you
don't want to count 0 for a lot of business hour metrics when a person regularly
starts working at 8am or regularly works until 6pm. We have found that setting
the range as 7am to 7pm eliminates most of those anomalies.

One still needs to limit the maximum "business hours" counted in a day to eight
hours, though, for most metrics.

Next: [Common Pitfalls When Designing Metrics](metric-pitfalls.md)
