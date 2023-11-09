# Developer Productivity and Happiness: Goals and Signals

This is a proposal, at the highest level, of what we try to measure to improve
the productivity of engineering teams. This should help guide the creation of
metrics and analysis systems. This is not a complete listing of every single
thing that we want to measure regarding developer productivity. It is an
aspirational description of _how_ we would ideally be measuring things and _how_
we should come up with new metrics.

It is based on the [Goals, Signals, Metrics system](goals-signals-metrics.md).
This document contains our primary Goals and Signals.

- [Goals](#goals)
  - [Productive](#productive)
  - [Happy](#happy)
  - [Not Limited to Tools and Infrastructure](#not-limited-to-tools-and-infrastructure)
- [Signals](#signals)
  - [Productive](#productive-1)
    - [Efficient](#efficient)
    - [Caution: Don't Compare Individual Efficiency](#caution-dont-compare-individual-efficiency)
    - [Effective](#effective)
    - [Over-Indexing On A Single Effectiveness Metric](#over-indexing-on-a-single-effectiveness-metric)
  - [Happy](#happy-1)

## Goals

The simplest statement of our goal would be:

Developers at LinkedIn are **productive** and **happy**.

That could use some clarification, though.

### Productive

What "productive" means isn't very clear, though—what are we actually talking
about? So, we can refine "Developers at LinkedIn are productive" to:

**Developers at LinkedIn are able to _effectively_ and _efficiently_ accomplish
their _intentions_ regarding LinkedIn's _software systems_**.

This is a more precise way of stating exactly what we mean by "productive." A
person is productive, by definition, if they produce products efficiently.
"Efficiently" implies that you want to measure something about how long it takes
or how often a product can be produced. So that means that we have to have a
time that we start measuring from, and a time that we stop measuring at. The
earliest point we can think of wanting to measure is the moment when the
developer directly _intends_ to do something (as in, the intention they have
right before they start to take action, not the first time they have some idle
thought), and the last moment is when that action is totally complete.

There are many different intentions a developer could have: gathering
requirements, writing code, running tests, releasing software, creating a whole
feature end-to-end, etc. They exist on different levels and different scopes.
It's "fractal," basically—there are larger intentions (like "build a whole
software system") that have smaller intentions within them (like "write this
code change"), which themselves have smaller intentions within them ("run a
build"), etc.

The goal also states "effectively," because we don't just care that a result was
_fast_, we care that the intention was _actually carried out_ in the most
complete sense. For example, if I can release my software quickly but my service
has 3 major production incidents a day, then I'm not as effective as I could be,
even if I'm efficient. It's reasonable to assume that no developer intends to
release a service that fails catastrophically multiple times a day, so that
system isn't accomplishing a developer's intention.

### Happy

Happy about what? Well, here's a more precise statement:

**Developers at LinkedIn are happy with the tools, systems, processes,
facilities, and activities involved in software development at LinkedIn.**

### Not Limited to Tools and Infrastructure

Note that although the primary focus of our team is on Tools & Infrastructure,
neither of these goals absolutely limit us to Tools & Infrastructure. If we
discover that something outside of our area is impacting developer productivity
in a significant way, like a facilities issue or process issue, we should feel
empowered to raise that issue to the group that handles that problem.

## Signals

Let's break down each goal by its parts.

### Productive

We'll break this down into signals for "effective" and signals for "efficient."

#### Efficient

Essentially, we want to measure the time between when a developer has an
intention and the time when they accomplish that intention. This is probably
best framed as: 

**The time from when a developer starts taking an action to when they accomplish
what they were intending to accomplish, with that action.**

It's worth remembering that there are many different types of intentions and
actions that a developer takes, some large, some small. Here are some examples
of more specific signals that you might want to examine:

* The time between when a developer encounters a problem or confusion and when
  they get the answer they are looking for (such as via docs, support, etc.).
* How long it takes from when developers start writing a piece of code to when
  it is released in production.

There are many other signals that you could come up with—those are just
examples.

It's also worth keeping in mind:

**The most important resource we are measuring, in terms of efficiency, is the
amount of time that software engineers have to spend on something.**

That's _sort of_ a restatement of the above signal, but it's a clearer way to
think about some types of specific signals. In particular, it considers the
whole sum of time spent on things. For example, these could be specific signals
that you want to measure:

- How much time developers actually spend waiting for builds each day.
- How much time developers spend on non-coding activities.

The general point is that we care more about the time that human beings have to
spend (or wait) to do a task, and less about the time that machines have to
spend.

And there are many, many more signals that you could come up with in this
category, too.

#### Caution: Don't Compare Individual Efficiency

Don't propose metrics, systems, or processes that are intended to rate the
efficiency of individual engineers. We [aren't trying to create systems for
performance ratings of employees](metrics-and-performance-reviews.md). We are
creating systems that drive our developer productivity work.

It's even worth thinking about whether or not your system _could_ be used this
way, and either prevent it from being used that way in how the system is
designed, or forbid that usage via cautions in the UI/docs.

#### Effective

Essentially, we want to know that when a developer tries to do something, they
actually accomplish the thing they were intending to accomplish. Things like
crashes, bugs, difficulty gathering information—these are all things that
prevent an engineer from being effective.

When problems occur in a developer's workflow, we want to know how often they
occur and how much time they waste. Probably the best high-level signal for this
would be phrased like:

**The probability that an individual developer will be able to accomplish their
intention successfully. (Or on the inverse, the frequency with which developers
experience a failure.)**

You have to take into account the definition of "success" appropriately for the
thing you're measuring. For example, let's say a developer, for some reason, has
the intention "I run all my tests and they pass." In that case, if a test fails,
they've failed to accomplish their intention. But most of the time, a developer
runs tests to know if the code they are working on is broken. So success would
be, "I ran the tests and they only failed if I broke them." Thus, flaky tests,
infrastructure failures, or being broken by a dependency would _not_ be the
developer accomplishing their intention successfully. Defining the intention
here is important.

We use _probability_ here because what we care about is how individual engineers
are actually impacted by a problem. For example, let's say you have a piece of
testing infrastructure that's flaky 10% of the time. What does that actually
mean for engineers? How often is an engineer impacted by that flakiness? Maybe
the system mostly just runs tests in the background that affect very few people.

In order to define this probability appropriately, you have to know what group
of engineers you're looking at. You could be looking at the whole company, or
some specific [persona](developer-personas.md), area, org, or team.

Some specific examples of possible signals here would be:

* The probability that when a developer runs a test in CI, it will produce valid
  results (that is, if it fails, it's not because of flakiness).
- The probability that a developer will run a build without the build tool
  crashing.
- How often (such as the median number of times per day) a developer experiences
  build tool crashes.

It's important to keep in mind here that what we care about most is what
developers actually experience, not just what's happening with the tool.

Very often, just knowing _how often_ something happens isn't enough to
understand its impact, though. You also might want to tie things back to
efficiency here, by noting:

**How much extra human time was spent as a result of failures.**

For example, it would be good to know that 15 engineers were caught up for three
days handling a production incident, wouldn't it? That changes the importance of
addressing the root causes, there. Some signals here could be:

- How much time was spent re-running tests after they had flaky failures.
- How much time a developer had to spend shepherding a change through the
  release pipeline due to release infrastructure failures.

Not all failures are black and white, though. Very often, an intention
_partially_ succeeds. For example, I might release a feature with a bug that
affects only 0.01% of my users. Thus, it is sometimes also useful to know:

**The percentage _degree_ of success of each action that a developer takes.**

For example, one way to look at flakiness is how many tests per run actually
flake. That is, if I have 10 tests in my test suite but only one fails due to
flakiness, then that specific run of that specific test suite had a 90% success
rate.

#### Over-Indexing On A Single Effectiveness Metric

It's important not to over-index on any one of these "effectiveness" signals.
Sometimes, the probability of a failure is low, but it is very impactful in
terms of human time when the failure occurs. It's helpful to have data for _all_
of the signals, as appropriate for the thing you're measuring.

### Happy

Usually, we rate happiness via subjective signals. Basically we want to know:

1. **The percentage of software engineers that are happy with the tools,
   systems, processes, facilities, and activities involved in software
   engineering at LinkedIn.**
2. **A score for _how_ happy those engineers are.**

And you can break it down for specific tools, systems, processes, and
facilities. Very often we say "satisfied" instead of happy, as a more concrete
thing that people can respond more easily to.

One of our assumptions is that if you improve the quantitative metrics in the
"Productive" section, you should increase developer happiness. If happiness
_doesn't_ increase, then that probably means there's something wrong with your
quantitative signals for productivity—either you've picked the wrong
signal/metric, or there's some inaccuracy in the data.
