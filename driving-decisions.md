# Driving Decisions With Data

It is important when designing metrics, systems, or processes involving data
that we understand how they will be used to drive what decisions, by who. The
data needs to be something that [engineering leadership, senior ICs, front-line
managers, or front-line engineers](audiences.md) can _do_ something effective
with.

**When you propose a metric, system, or process involving data, you should
always explain how it will drive decisions.**

- [Bad Examples](#bad-examples)
  - [Misleading Numbers](#misleading-numbers)
  - [No Audience](#no-audience)
- [Good Example](#good-example)
- [Driving Decisions Differently for Different Groups](#driving-decisions-differently-for-different-groups)
- [Focus on Causing Action](#focus-on-causing-action)

## Bad Examples

Let's look at some bad examples to demonstrate this.

### Misleading Numbers

Most of us know that "lines of code written per software engineer" is a bad
metric. But it's especially bad in this context of effectively driving the right
decisions.

_Who_ does _what_ with that number? It tells nothing to engineering leadership
and senior engineers--there is no specific action they can take to fix it. The
front-line engineers don't care that much, other than to look at their own stats
and feel proud of themselves for having written a lot of code. It's only the
front-line managers who will be able to _do_ something with it, by trying to
talk to their engineers or figure out why some of their engineers are more
"productive" than others.

Now, to be clear, it's fine to make a metric, system, or process that only one
of these groups can use. The problem with _this_ metric is that when you give it
to a front-line manager, it often either (a) misleads them or (b) is useless.
They may see that one engineer writes fewer lines of code than another, but the
engineer writing fewer lines actually has more impact on the users of the
product, or is doing more research, or is writing better-crafted code.

Basically, what you've actually done is sent the front-line manager on an
unreliable wild-goose chase that wasted their time and taught them to distrust
your metrics and you! You drove no decision for that manager--in fact, you
instead [created a problem](data-vs-insights.md) that they have to solve:
constantly double-checking your metric and doing their own investigations
against it, since it's so often wrong. Worse yet, if the manager trusts this
metric without any question, it could lead to bad code, rewarding the wrong
behavior, a bad engineering culture, and low morale.

### No Audience

Another way to do this wrong is to have some metric but not have any
[_individual_ who will make a decision based on it](audiences.md). For example,
measuring test coverage on a codebase that nobody works on would not be very
useful.

## Good Example

1. You discover, through surveys or other valid feedback mechanisms, that mobile
   developers feel their releases are too slow. 
2. You properly instrument the release pipeline to accurately measure the length
   of each part of the pipeline. 
3. You do some basic investigation to see what the major pain points are that
   cause this slowness along each part of the pipeline, to get an idea of how
   much work would be involved in actually fixing each piece, and what would be
   the most important pieces to fix first. 
4. You boil this information down into an understandable report that concisely:
    * Proves the problem exists
    * Explains why it's important
    * Gives a birds-eye view of where time is being spent in the release
      pipeline
    * Provides very rough estimates of how much work it is to solve each piece
5. This report is presented to [engineering leadership](audiences.md), who
   decides who to assign, at what priority, to fix the most important parts of
   the release pipeline to address this issue.
6. Front-line engineers use the instrumentation we developed in order to
   understand and solve the specifics of the problem.
7. After the work is done, the same data can be referenced to show how
   successful the optimizations were.

## Driving Decisions Differently for Different Groups

At the level of front-line managers and front-line engineers, it is sufficient
to provide information that allows people to figure out _where_ a problem is, so
that front-line engineers can track down the actual problem and solve it. This
can sometimes be [more "data" and less "insights."](data-vs-insights.md)

At more senior levels, [more "insights" are required as opposed to raw
data](data-vs-insights.md). In general, the more senior a person you are
presenting to, the more work you should have done up front to provide insights
gathered from data, as opposed to just showing raw data.

## Focus on Causing Action

When you deliver data or insights to people, it should actually be something
that will influence their decisions. They should be interested in having data
for their decisions, and be willing to act based on the data. It's important to
check this _up front_ before doing an analysis--otherwise, you can end up doing
a lot of analysis work that ends up having no impact, because the recipient was
never going to take action on it in the first place.

For example, sometimes teams have mandates of things they _must_ do, such as
legal or policy compliance, where it doesn't matter what you say about the work
they do, they still have to do it in exactly the way they plan to do it. It's
not useful to try to change their mind with data--your work will not result in
any different decision.

In general, if a person has already made up their mind and no data or insight
will realistically sway them, it's not worth doing the work to provide them data
or insights. We might have some opinion about the way the world should be, but
that doesn't matter, because a _person has to change their mind_ in order for
action to happen. If we won't even _potentially_ change somebody's mind, we
should not do the work.

It can be useful to ask people who request data:

1. What do you think the data will say? (What is their prediction before they
   look at the data.)
2. If it is different than what you think, will that change your decision in any
   way?

If the answer to question #2 is "no," then it's not worth working on that
analysis.