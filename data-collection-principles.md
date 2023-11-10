# Data Collection Principles

Teams who make metrics and do data analysis often wonder: how much data should I
collect? How long should I retain it for? Are there important aspects of how I
should structure the data?

In general, the concepts here are:

1. Collect as much data as you possibly can. This becomes the "lowest layer" of
   your data system.
2. Refine that, at higher "layers," into data stores designed for specific
   purposes.
3. Always be able to understand how two data points connect to each other,
   across any data sets. (That is, always know what your "join key" is.)

For example, imagine that you are collecting data about your code review tool.

Ideally, you record every interaction with the tool, every important touchpoint,
etc. into one data set that knows the exact time of each event, the type of
event, all the context around that event, and important "join keys" that you
might need to connect this data with other data sources (for example, the ID of
commits, the IDs of code review requests, the username of the person taking
actions, the username of the author, etc.).

Then you figure out specific business requirements you have around the data. For
example, you want to know how long it takes reviewers to respond to requests for
review. So you create a higher-level data source, derived from this "master"
data source, which contains only the events relevant for understanding review
responses, with the fields structured in such a way that makes answering
questions about code review response time really easy. 

That's a basic example, but there's more to know about all of this.

- [When In Doubt, Collect Everything](#when-in-doubt-collect-everything)
- [Purpose](#purpose)
- [Boundaries, Intentions, and Join Keys](#boundaries-intentions-and-join-keys)

## When In Doubt, Collect Everything

It is impossible to go back in time and instrument systems to answer a question
that you have in the present. It is also impossible to predict every question
you will want to answer. You must _already have_ the data.

As a result, you should strive to collect every piece of data you can collect
about every system you are instrumenting. The only exceptions to this are:

1. Don't collect so much data that it becomes extremely expensive to store, or
   _very_ slow to query. Sometimes there are low-value events that you can
   pre-aggregate, only store a sample of, or simply skip tracking at all. Note
   that you have to actually prove that storage would be expensive or
   slow---often, people _believe_ something will be expensive or slow when it's
   really not. Storage is cheap and query systems can be faster than you expect.
2. Some data has security or privacy restrictions. You need to work with the
   appropriate people inside the company to determine how this data is supposed
   to be treated.

As an extreme example, you could imagine a web-logging system that stored the
entirety of every request and response. After all, that's "everything!" But it
would be impossible to search, impossible to store, and an extremely complex
privacy nightmare.

The only other danger of "collecting everything" is storing the data in such a
disorganized or complicated way that you can't make any sense of it. You can
solve that by keeping in mind that no matter what you're doing, you always want
to produce [insights](data-vs-insights.md) fron the data at some point. Keep in
mind a few questions that you know people want to answer, and make sure that
it's at least theoretically possible to answer those questions with the data
you're collecting, with the fields you have, and with the format you're storing
the data in.

If your data layout is well-thought-out and provides sufficient coverage to
answer almost any question that you could imagine about the system (even if it
would take some future work to actually understand the answers to those
questions) then you should be at least somewhat future-proof.

## Purpose

In general, you always want to have some idea of why you are collecting data. At
the "lowest level" of your data system, the telemetry that "collects
everything," this is less important. But as you derive higher-level tables from
that raw data, you want to ask yourself things like:

1. What questions are people going to want to answer with this data?
2. _Why_ are people going to ask those questions? How does answering those
   questions help people? (This gives you insight into how to present the data.)
3. What dimensions might people want to use to slice the data?

This is where you take the underlying raw data and massage it into a format that
is designed to solve specific problems. In general, you don't want to expose the
underlying complex "collect everything" data store to the world. You don't even
want to expose it directly to your dashboards. You want to have simpler tables
_derived from_ the "everything" data store---tables that are designed for some
specific purpose.

You can have a hierarchy of these tables. Taking our code review example:

1. You start off with the "everything" table that contains time series events of
   every action taken with the tool. 
2. From that, you derive a set of tables that let you view just comments,
   approvals, and new code pushes, with the "primary key" being the Code Review
   ID (so it's easy to group these into actions that happened during a
   particular code review process). 
3. Then you want to make a dashboard that shows how quickly reviewers responded
   on each code review. You could actually now make one table that just contains
   the specific derived information the dashboard needs.

You'll find that people rarely ever want to directly query the table from Step 1
(because it's hard to do so) sometimes want to query the table from Step 2, and
the table from Step 3 becomes a useful tool in and of itself, even beyond just
the dashboard. That is, the act of creating a table specifically for the
dashboard makes a useful data source that people sometimes want to query
directly.

Sometimes, trying to build one of these purpose-built tables will also show you
gaps in your data-collection systems. It can be a good idea to have one of these
purpose-built tables or use cases in mind even when you're designing your
systems for "collecting everything," because they can make you realize that you
missed some important data.

In general, the better you know the requirements of your consumers, the better
job you can do at designing these purpose-built tables. It's important to
understand the current and potential requirements of your consumers when you
design data-gathering systems. This should be accomplished by actual research
into requirements, not just by guessing.

## Boundaries, Intentions, and Join Keys

It should be possible to know when a large workflow starts, and when it ends. We
should know that a developer intended something to happen, the steps involved in
accomplishing that intention, when that whole workflow started, and when it
ended. We should not have to develop a complex algorithm to determine these
things from looking at the stored data. The stored data should contain
sufficient information that is very easy to answer these questions.

We need to be able to connect every event within a workflow as being part of
that workflow, and we need to know its boundaries---its start point and end
point.

For example, imagine that we have a deployment system. Here's a set of events
that represent a _bad_ data layout:

1. User Alice requested that we start a deployment workflow named "Deploy It" at
   10:00.
2. Binary Foo was started on Host Bar at 10:05.
3. Binary Baz was started on Host Bar at 10:10.
4. Binary Baz responded "OK" to a health check at 10:15.
5. Binary Foo responded "OK" to a health check at 10:20.

We have no idea that "Deploy It" means to deploy those two binaries. What if
there are a hundred simultaneous workflows going on? What if "Deploy It" has
been run more than once in the last five minutes? We have no idea that those
health checks signal the end of the deployment. In fact, _do_ they signal the
end of the deployment? Are there other actions that "Deploy It" is supposed to
do? I'm sure the author of "Deploy It" knows the answers to that, but we, a
central data team, have _no way_ of knowing that, because it's not recorded in
the data store.

A better data layout would look like:

1. User Alice started the deployment workflow "Deploy It" at 10:00. This
   indicates an intent to deploy Binary Foo and Binary Baz to 200 machines. We
   give this specific instance of the workflow an ID: "Deploy It 2543."
2. We record all of the actions taken by "Deploy It 2543" and be sure to tag
   them in our data store witih that ID.
3. The deployment workflow itself contains a configuration variable that allows
   users to specify how many hosts the machine must successfully deploy to
   before we consider the deployment "successful." For example, let's say this
   one requires only 175 hosts to be deployed to be "successful." Once 175 hosts
   are deployed, we record an event in the data store indicating successful
   completion of the deployment workflow. (We also record failure in a similar
   way, if the workflow fails, but noting that it's a failure along with any
   necessary details about the failure.)

You don't have to figure out every workflow in advance that you might want to
measure. When you know a workflow exists, record its start and end point. But
even when you don't know that a workflow exists, make sure that you can always
see _in the data store_ that two data points are related when they are related.
For example, record that a merge is related to a particular PR. Record that a
particular PR was part of a deployment. Record that an alert was fired against a
binary that was part of a particular deployment. And so forth. Any two objects
that _are_ related should be able to be easily connected by querying your data
store.

Next: [Principles and Guidelines for Metric Design](metric-principles.md)