# Goals, Signals, and Metrics

There is a framework we use for picking metrics called “Goals-Signals-Metrics.” 

Basically, first you decide what the **goals** are that you want to achieve for
your product or system. Then you decide on the **signals** you want to examine
that tell you if you’re achieving your goal--essentially, these are what you
would measure if you had perfect knowledge of everything. Then you choose
**metrics** that give you some proxy or idea of that signal, since few signals
can be measured perfectly.

## Goals

A goal should be framed as the thing that you want your team, product, or
project to accomplish. It should not be framed as "I want to measure X."

**Most of the trouble that teams have in defining metrics comes from defining
unclear goals.**

_Webster's Third New International Dictionary_ defines a "goal" as: 

> The end toward which effort or ambition is directed; a condition or state to
> be brought about through a course of action.

This needs to be stated in a fashion specific enough that it _could be
measured_. Not that you have to know in advance what all the metrics will be,
but that conceptually, a person could know whether you were getting closer to
(or further from) your goal.

### Example Goal

In developing a goal, you can start with a vaugue statement of your desire. For
example:

**LinkedIn's systems should be reliable.**

However, that's not measurable. So the first thing you do is **clarify
definitions**. 

First off, what does "LinkedIn's systems" mean? What does "reliable" mean? How
do we choose which of our systems we want to measure? 

Well, to figure this out, we have to ask ourselves **why** we have this goal.
The answer could be "We are the team that assures reliability of all the
products that are used by LinkedIn's users." In that case, that would clarify
our goal to be:

**The products that are used by LinkedIn's users should be reliable.**

That's still not measurable. Nobody could tell you, concretely, if you were
accomplishing that goal. Here's the remaining problem: what does "reliable"
mean?

Once again, we have to ask ourselves **why** we have this goal. To do this, we
might look at the larger goals of the company. At LinkedIn, our [top-level
vision](https://about.linkedin.com/) is: "Create economic opportunity for every
member of the global workforce." This gives us some context to define
reliability: we somehow want to look at  things that prevent us from
accomplishing that vision. Of course, in a broad sense, there are _many_ factors
that could prevent us: social, cultural, human, economic, etc. So we say, well,
our scope is what we can do _technically_ with our software development and
production-management processes, systems, and tools. What sort of technical
issues would members experience as "unreliability" in that context? Probably
bugs, performance issues, and downtime.

So we could update our goal to be:

**LinkedIn's users have an experience of our products that is free from bugs,
performance issues, and downtime.**

We could get more specific and define "bug," "performance issue," and
"downtime," if it's not clear to the team what those specifically mean. The
trick here is to get something that's clear and measurable, without it being
super long. What I would recommend, if you wanted to clarify those terms, is to
create _sub-goals_ for each of those terms. That is, keep this as the overall
goal, and then state three more goals, one for bugs, one for performance issues,
and one for downtime, which do a better job of spelling out what each of those
means.

One of the things that you'll notice about this exercise is that not only does
it help us define our metrics, it actually helps clarify what is the most
important work we should be doing. For example, this goal tells us that we
should be paying _more_ attention to the experience of our users than the
specific availability numbers of low-level services (even though we might care
about those, too).

### Uncertainty

**If you aren’t sure how to measure something, it’s very likely that you haven’t
defined what it is that you are measuring.**  This was the problem with
"developer productivity" measurements from the past--they didn’t define what
“developer productivity” actually meant, concretely, exactly, in the physical
universe. They attempted to measure an abstract nothing, so they had no real
metrics. This is why it is so important to understand and clarify your goals
before you start to think about metrics.

## Signals

Signals are what you would measure if you had perfect knowledge---if you knew
everything in the world, including everything that was inside of everybody
else's mind. These do not have to actually be measurable. They are a useful
mental tool to help understand the areas one wants to measure. 

Signals are the answer to the question, "How would you know you were achieving
your goal(s)?"

For example, some signals around reliability might be:

* Human effort spent resolving production incidents.
* Human time spent debugging deployment failures.
* Number of users who experienced a failure in their workflow due to a bug
* Amount of time lost by users trying to work around failures.
* How reliable LinkedIn's products are according to the _belief_ of our users.
* User-perceived latency for each action taken by users.

The concept of "signals" can also be useful to differentiate them from "metrics"
(things that can actually be measured). Sometimes people will write down a
signal in a doc and then claim it is a metric, and this distinction in terms can
help clarify that.

## Metrics

Metrics are numbers over time that can actually be measured. A metric has the
following qualities:

* It can actually be implemented, in the real world, and produce a concrete
  number.
* The number can be trended over time.
* It is meaningful when the number goes up or goes down, and that meaning is
  clear.

All metrics are _proxies_ for your signal. There are no perfect metrics. It is a
waste of time to try to find the "one true metric" for anything. Instead, create
multiple metrics and triangulate the truth from looking at different metrics.
All metrics will have flaws, but _sets_ of metrics can collectively provide
insight.

Example metrics for our "reliability" goal from above might be something like:

* The percentage of user sessions that do not experience an error as determined
  by our product telemetry.
* Percentage of deployments that do not experience a failure requiring human
  intervention.
* Conduct a survey of a cross-section of users to ask them their opinion about
  our reliability, where they give us a score, and aggregate the scores into a
  metric.
* Define what the "acceptable" highest latency would be for each UI action, and
  then count how often UI interactions happen _under_ those thresholds. (Display
  a percentage of how many UI interactions have an "acceptable" latency.)

If you look at our signals above, you will see that some of these map back to
our signals.

Overall, there is a _lot_ to know about metrics, including what makes metrics
good or bad, how to take action on them, what types of metrics to use in what
situation, etc. It would be impossible to cover all of it in this doc, but we
attempt to cover some of it in other docs on this site.