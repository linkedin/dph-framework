# Audiences: Always Know Who Your Data Is For

When designing any system for metrics or data collection, you need to know who
your _audience_ is. Otherwise, it is hard to get _action_ to be taken on the
data.

For example, let's take the metric "number of pastries consumed by employees."
If you're the pastry chef at the company cafeteria, that's an interesting
metric. If you're the head of Engineering, it's not an interesting metric.

Ultimately, all our work serves _people_. Any organization is basically just an
agreement between people. The pieces of the organization that actually exist in
the physical universe are material objects (buildings, computers, etc.) and
_individuals_. We serve individuals.

For engineering metrics and feedback systems, there are a few broad categories
of individuals that we serve, who have very different requirements. How we
provide [data and insights](data-vs-insights.md) to these audiences is very
different for each audience.

**When you propose a metric, system, or process, you should always say which of
the groups below you are serving and how you are serving them.**

- [Front-Line Developers](#front-line-developers)
- [Front-Line Managers](#front-line-managers)
- [Engineering Leadership](#engineering-leadership)
- [Tool Owners](#tool-owners)
- [Productivity Champions](#productivity-champions)
- [Levels of Metrics](#levels-of-metrics)

## Front-Line Developers

A "front-line developer" is any person who directly writes or reviews code.

Developers are best served by delivering [insights](data-vs-insights.md) to them
within their natural workflow. For example, insights that directly help them
during a code review, displayed in the code review tool. Imagine if we could
tell a developer, "This change you are about to make will increase the build
time of your codebase by 50%." Those are the sort of insights that most help
developers---actionable information displayed right when they can act on it.

Developers also need [data](data-vs-insights.md) when they are making decisions
about how to do specific work (such as "what's the most important performance
problem to tackle for my users?" or "how many users are being affected by this
bug?"). Developers do not usually need [metrics](goals-signals-metrics.md) in
dashboards. Instead, they need analytical tools---systems that allow them to
dive into data or debug some specific problem.

Note that this is actually the _largest_ group of people that we serve, and
actually the place where we can often make the most impact. It’s easy to
consider that because Directors and VPs are "important people" that it is more
important to serve them, but **we move more of the organization and make more
change by providing actionable insights to developers who are doing the actual
work of writing our systems**.

## Front-Line Managers

By this, we mean managers who directly manage teams of developers. Often,
managers of managers have similar requirements to front-line managers, and so
could also covered as part of this audience.

We provide [data](data-vs-insights.md) that front-line managers can use to form
their own insights about what their team should be working on or how they should
prioritize work on their team. Front-Line Managers usually have the time (and
desire) to process the data relevant to their team and turn it into insights
themselves. We do also provide _some_ insights that front-line managers can use
directly to inform their decisions.

Managers tend to have a regular cadence of meetings where they can look at
dashboards, so putting [metrics](goals-signals-metrics.md) in dashboards is
helpful for them.

The information we provide for front-line managers should feed into decisions as
small as "what should we work on for the next two weeks?"

## Engineering Leadership

By "engineering leadership," we usually mean SVPs, VPs, Sr. Directors, and
Directors in Engineering. This can also include very senior engineers at the
company who will have similar requirements (though they also end up fitting into
multiple other audiences, as well). Essentially, this category includes anybody
who is distant from the day-to-day details of the thing they are in charge of. 

We provide [insights](data-vs-insights.md) to engineering leadership that
either:

1. Allow them to choose what direction the organization should go in, or
2. Convince them what direction to go in based on sound reasoning we provide
   (which usually would mean an argument based on data). 

The result here should be that an engineering leader does one of these three
things:

1. Tells actual people to go do actual work.
2. Decides that no work needs to be done.
3. Decides on the _prioritization_ of work--deciding _when_ work will be done,
   by who.

Engineering Leaders often just need a system that shows them that a problem
_exists_, so that they can ask for a more detailed investigation to be done by
somebody who reports to them.

The decisions made at this level are usually _strategic_ decisions--at the
shortest, multi-week, at the longest, multi-year, and so the insights we provide
to engineering leadership should guide decisions at that level.

## Tool Owners

This is a manager or senior developer whose team works on developer tools or
infrastructure.

Tool Owners need [data and insights](data-vs-insights.md) that help them
understand their users and how to make the most impact with their
infrastructure. When in doubt, err on the side of data instead of insights,
because the requirements of Tool Owners are complex, and they often can spend
the time to dive into the data themselves.

Tool Owners need analytical systems that allow them to dive into data to
understand the specifics of tool usage, workflows, problems developers are
having, etc. While Front-Line Developers need such tools to analyze their own
codebases, Tool Owners need these tools for analyzing _the whole company_. 

For example, an owner of the build tool might need to ask, "Which team is having
the worst build experience?" They would need to be able to define what "worst
build experience" means themselves (so basically, just slicing the data any way
they need to). Then, they would need to understand the detailed specifics of
what is happening with individual builds, so their teams can write code to solve
the problem.

Tool Owners are also benefited by having [metrics](goals-signals-metrics.md) in
dashboards. They may need many metrics (maybe 10 or more) to be able to
understand if the experience of their users are getting better or worse. At any
given time, their teams might be focused on one or two metrics, but usually the
front-line developers _within_ the Tool Owner team will need to look at other
metrics to do complete investigations.

## Productivity Champions

This is a person who cares about the developer productivity of a team or a set
of teams, and takes it as their responsibility to do something about it
directly, advise a senior executive what to do about it, or encourage other
teams to take action on it.

We don’t think of this person as a Tool Owner (even though one person may on
rare occasion be both a Tool Owner and a Productivity Champion). 

This audience has the most complex set of requirements. Essentially, they need
all the tools of all the other audiences, combined. They need to look at broad
overviews of data to understand where there are problems, and then they need
detailed dashboards and analytical tools to dive into the specifics of the
problem, themselves.

## Levels of Metrics

When desgining [metrics](goals-signals-metrics.md), there is another thing to
think about besides the above audiences, which is "what level of the org chart
is this audience at?" For example, the entire developer tools org might have a
set of metrics that measure the overall success of that org. However, individual
teams within that org would have more detailed, lower-level metrics.

In general, teams should know what their top-level metrics are---what are the
most important metrics that they are driving and which measure how well they are
achieving their [goals](goals-signals-metrics.md). There can be many top-level
metrics, so long as they are a good representation of the aggregate
accomplishments of the team toward the team's goals. 

There can be many other metrics that a team has besides their top-level metrics.
Front-line developers might need a large set of metrics to be able to judge the
effectiveness of their changes or what area should be worked on next. The
reasons to have top-level metrics are:

1. So that a team can focus on specific numbers that they are driving---this is
   one of the most effective ways to get action taken on metrics, is to focus a
   team around "these are the numbers we are driving."
2. So that people don't have to look at _so many_ graphs that each graph
   individually becomes meaningless. No matter how smart a leader is, they can't
   look at 100 graphs _simultaneously_ and make any sensible decision about
   them. They _could_ look at 10 graphs, though.

We call the top-level metrics of a team the "Key Impact Metrics."