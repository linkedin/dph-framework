# Common Pitfalls When Designing Metrics

There are some common pitfalls that teams fall into when the start trying to
measure developer productivity, the success of their engineering efforts, etc.
It would be impossible to list every way to "do it wrong," but here are some of
the most common ones we've seen.

- [Measuring Whatever You Can Measure](#measuring-whatever-you-can-measure)
- [Measuring Too Many Things](#measuring-too-many-things)
- [Measuring Work Instead of Impact](#measuring-work-instead-of-impact)
- [Measuring Something That is Not Acted On](#measuring-something-that-is-not-acted-on)
- [Defining Signals and Calling them "Metrics"](#defining-signals-and-calling-them-metrics)
- [If Everybody Does This, We Can Have a Metric!](#if-everybody-does-this-we-can-have-a-metric)
- [Metrics That Create a Mystery](#metrics-that-create-a-mystery)
- [Vanity Metrics](#vanity-metrics)

## Measuring Whatever You Can Measure

When a team first starts looking into metrics, often they just decide to measure
whatever is easiest to measure---the data they currently have available. Over
time, this metric can even become entrenched as "the metric" that the team uses.

There are lots of problems that occur from measuring whatever number is handy.

For example, it's easy for a company to measure only revenue. Does that tell you
that you're actually accomplishing the goal of your company, though? Does it
tell you how happy your users are with your product? Does it tell you that your
company is going to succeed in the long term? No.

Or let's say you're a team that manages servers in production. What if you only
measured "hits per second" on those servers? After all, that's usually a number
that's easy to get. But what about the reliability of those servers? What about
their performance, and how that impacts the user experience? Overall, what does
this have to do with the goals of your team?

The solution here is to [think about your goals](goals-signals-metrics.md) and
derive a set of metrics from those, instead of just measuring whatever you can
measure.

## Measuring Too Many Things

If you had a dashboard with 100 graphs that were all the same size and color, it
would be very hard for you to determine which of those numbers was important. It
would be hard to focus a team around improving specific metrics. Everybody would
get lost in the data, and very likely, no action would be taken at all.

This is even worse if those 100 graphs are spread across 20 different
dashboards. Everybody gets confused about where to look, which dashboard is
correct (when they disagree), etc.

The solution here is to have fewer dashboards that have a small set of relevant
metrics on them, by understanding your [audience](audiences.md) and what [level
of metrics](audiences.md) you're showing to each audience.

## Measuring Work Instead of Impact

Would "number of times the saw moved" be a good metric for a carpenter? No.
Similarly, any metric that simply measures the _amount of work_ done is not a
good metric. It gets you an organization that tries to make work _more
difficult_ so they can show you that they did _more of it_.

Often, people measure work when they do not understand the _job function_ of the
people being measured. In our carpenter example, the job function of a carpenter
who builds houses is very different from a carpenter who repairs furniture. They
both work with wood and use some of the same tools, but the _intended output_ is
very different. A house builder might measure "number of projects completed that
passed inspection," while the repairman might measure, "repaired furniture
delivered to customers." 

Instead of measuring work, you want to focus on [measuring the impact or result
of the work](metric-principles.md). In order to do this, you have to understand
the [goals](goals-signals-metrics.md) of the team you are measuring.

## Measuring Something That is Not Acted On

Sometimes we have a great theory about some metric that would help somebody. But
unless that metric has an [audience](audiences.md) that will actually [drive
decisions](driving-decisions.md) based on it, you should not implement the
metric.

Even when it has an audience, sometimes that audience does not actually plan to
act on it. You can ask, "If this metric shows you something different than you
expect, or if it starts to get worse, will you change your course of action?" If
the answer is no, you shouldn't implement the metric.

## Defining Signals and Calling them "Metrics"

Sometimes you will see a document with a list of "metrics" that can't actually
be implemented. For example, somebody writes down "documentation quality" or
"developer happiness" as proposed metrics, with no further explanation.

The problem is that these are not [metrics](goals-signals-metrics.md), they are
[signals](goals-signals-metrics.md). They will never be implemented, because
they are not concretely defined as something that can be specifically measured.

If you look at a "metric" and it's not _immediately clear_ how to implement it,
it's probably a signal, and not a metric.

## If Everybody Does This, We Can Have a Metric!

Don't expect people to change their behavior _just_ so you can measure it. 

For example, don't expect that everybody will tag their bugs, PRs, etc. in some
special way _just_ so that you can count them. There's no incentive for them to
do that correctly, no matter how much _you think_ it would be good. What really
happens is you get very spotty data with questionable accuracy. Nobody believes
your metric, and thus nobody takes action on it. And probably, they shouldn't
believe your metric, because the data will almost certainly be missing or wrong.

Sometimes people try to solve this by saying, "we will just make it mandatory to
fill out the special tag!" This does _not_ solve the problem. It creates a
roadblock for users that they solve by putting random values into the field
(often just whatever is easiest to put into the field). You can start to engage
in an "arms race," where you keep trying to add validation to prevent bad data.
But why? At some point, you are actually _harming_ productivity in the name of
measuring it.

If you want people to change their behavior, you need to figure out a change
that would be beneficial to them or the company, not just to you. Otherwise, you
need to figure out ways to measure the behavior they currently have.

## Metrics That Create a Mystery

Metrics should help [solve a mystery](data-vs-insights.md), not create one.

The basic problem here is when a viewer says, "I don't know [what this metric
means when it goes up or down](metric-principles.md)." For example, counting the
total number of bugs filed in the company creates this sort of mystery. Is it
good when it goes up, because we have improved our QA processes? Is it good when
it goes down, because we have a less buggy system? Or (as usually happens) does
it just mean some team changed the administrative details of how they track
bugs, and thus the upward or downward movement is meaningless?

The most common offenders here are [metrics that aggregate multiple mumbers into
a score](scores.md).

## Vanity Metrics

Metrics must [drive decisions](driving-decisions.md). That means they must show
when things are going well and when they are not going well. It is _especially_
important that they indicate when things are not going well, because those are
your opportunities for improvement! If a metric hides problems, it is actually
harmful to the team's goals.

Imagine counting "number of happy customers" as your only metric. In January, I
have 100 customers, and 10 of them are happy. In February, I have 200 customers,
and 15 of them are happy. Our metric goes up, but our actual situation is
getting worse!

Sometimes teams are worried about metrics that "make them look bad." But
look---if things are bad, they are bad. Only by acknowledging that they are bad
and working to improve them will anything actually get better. By hiding the
badness behind a vanity metric, we are worsening the situation for the company
and our customers.

Especially with developers, it is very hard to fool them. They _know_ when
things are bad. If you show them some beautiful number when they are all
suffering, all that will happen is you will damage your
[credibility](https://www.codesimplicity.com/post/effective-engineering-productivity/)
and nobody will ever believe you again in the future.