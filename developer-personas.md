# Developer Personas

We segment developers into "personas" based on their development workflow.

- [Why Personas?](#why-personas)
- [How to Define Personas](#how-to-define-personas)
  - [Define the Categories](#define-the-categories)
    - [Sub-Personas](#sub-personas)
  - [Initial Research](#initial-research)
  - [Categorizing Developers Into Personas](#categorizing-developers-into-personas)
    - [Example Personas](#example-personas)
- [What To Do With Personas](#what-to-do-with-personas)
  - [What About Using Personas For Quantitative Metrics?](#what-about-using-personas-for-quantitative-metrics)

## Why Personas?

It's very easy to assume, as somebody who works on developer productivity, that
one knows all about software development—after all, one is a software developer!
However, it turns out that different types of development require very different
workflows. If you've never done mobile development, web development, or ML
development, for example, you might be very surprised to learn how different the
workflows are!

One of the most common mistakes that developer productivity teams make is only
focusing on the largest group of developers at the company. For example, many
companies have _far_ more backend server engineers than they have mobile frontend
engineers, and so they assume that most (or all) of the developer productivity
work should go toward those backend engineers.

What this misses out on is the _importance to the business_ of the various
different types of developers at the business. You might only employ a few
mobile engineers, but how much impact does their work have for your customers?
Similarly, Machine Learning Engineers have a _very_ different workflow and set
of pain points from backend server developers—in fact, there's often no overlap
at all in their pain points and commonly-used tools. But in many companies
today, machine learning and AI are key to the success of their business.

If your developer productivity team has been focusing on only one type of
developer, and it seems like some parts of the company are very upset with you,
this might be why.

## How to Define Personas

### Define the Categories

We segment developers into _broad_ categories by their _workflow_. Obviously,
each developer works in a slightly different way. But you will find groups that
have large things in common in terms of the *type* of work that they do.

For example, you may see that there are a large group of developers who all work
in Java making "backend" servers. They might use different frameworks in Java,
different editors, different CI systems, or even different deployment platforms.
But you'll find that a _lot_ of their tooling is common within the group, or
fits into 2-3 categories (like one team uses The New CI System and another team uses
The Old CI System).

Since we use this data for survey analysis (as described below) we try to have
our Persona groups be large—at least 200 people, so that if only a small
percentage respond to the survey, we can still get statistically significant
data about the persona as a whole. Of course, if your company is smaller, you
might be doing interviews instead of surveys, in which case the personas should
be whatever size makes sense for you. The key is: don't have _too many_
personas, becasue that makes survey analysis hard. We currently have ten
developer personas for an engineering org with thousands of people in it, and
that number has seemed manageable.

Of course, if you have a small or medium-sized engineering team, you won't be
able to get groups of 200 people (that might be larger than your whole
engineering team!). If so, segment them out by the workflows that are most
important to the business.

#### Sub-Personas

People often ask if they can split the personas down even further and have
"sub-personas." Sure, you can totally do that. For example, you might have one
overall persona for people whose job it is to maintain production systems
(called SREs, DevOps Engineers, or System Administrators). However, you might
have one large sub-group that works on creating _tools_ for production
management, and another large sub-group that works on handling major incidents
in production. Those could be two sub-personas, because their workflows and
needs are very different, even though they have _some_ things in common.

The key here is to not make your survey analysis too complex. If the person
doing the survey analysis thinks there is value in separating out feedback and
scores for the SRE persona into these two categories, that's fine. However, you
might want to still review both of these sub-personas in the same meeting or
document or whatever process you decide on for doing your survey analysis.

### Initial Research

Once you have some idea of what categories exist, you'll likely want to do some
initial research into the current workflows of those engineers. Don't go too
overboard with this. It often is enough just to interview a set of engineers
(not just managers or executives) who are members of that persona. You'll want
to ask them about their workflows and what parts of that workflow are the most
frustrating. This should be a live dialogue, not an email or a survey, so that
you can ask follow up questions to clarify. You will also learn what questions
you should ask to this persona in future surveys.

Then you can synthesize the collected information into a document, and present
this document to the relevant stakeholders.

One thing that can be useful here is simply describing what the usual workflow
is for this type of developer. This is useful because when a tool developer
wants to support all the personas at the company, they can start off by reading
the descriptions that you've written, instead of having to figure out those
workflows themselves all over again.

You'll also want to try to get a count of how many people are in each persona,
even just an approximation, as this question comes up frequently, in our
experience.

### Categorizing Developers Into Personas

Now you will need some sort of system that categorizes developers into personas.
That is, some system that will tell you what personas a person is part of. Don't
create a system where managers or engineers have to fill out this data manually.
It will get out of date or be missing data. Instead, there are multiple data
sources you can combine to figure this out:

* A person's title.
* A person's management chain.
* The "cost center" that they belong to (usually tracked by your Finance team).
* Which systems / tools they use (possibly taking into account _how much_ they
  use them).
* What codebases or file types they contribute to (or review).

When you're starting off, it is simplest to start off with whatever data is
easiest to get, and accept some percentage of inaccuracy in the system. (For
example, we accepted a 10% inaccuracy in the early days of our Personas system,
and it didn't cause any real problems.)

Note: One developer can have multiple personas, that's fine. Sometimes people
ask if we should have a "master" persona for each person, but _usually_ when we
investigate, we discover the requester has misunderstood the purpose of
personas, or they are trying to work around a limitation in some other system.
Usually when a person has multiple personas, it's because they genuinely work in
all those workflows. Of course, it's always possible a valid use case for the
"master persona" concept comes up at some point in the future.

#### Example Personas

Here are some of the personas we have defined at LinkedIn:

* Backend Developer
* Data Scientist
* Machine Learning / AI Engineer
* Android Developer
* iOS Developer
* SRE
* Tools Developer
* Web Developer

Plus we have two other personas that are unique to how our internal systems
work (they are not included here because that would require too much explanation
for too little value).

## What To Do With Personas

For us, the Developer Personas system is used primarily as part of our survey
analysis, to split out pain points by developer persona.

We have a person called a "Persona Champion" who is a member of that persona
(for example, for the "Backend Developer" persona, the Persona Champion is a
backend developer). They do the analysis of the comments and the survey scores,
and work with infrastructure teams to help them understand the needs of that
Persona.

It is helpful to have a person who is familiar with the tools and workflow of
the persona doing the analysis, because they can pick up important details that
others will miss, and they have the context to "fill in the gaps" of vague or
incomplete comments. (Or, they know who they can go talk to to fill in those
gaps, because they know other developers who share their workflow.)

For more about persona champions, see the [detailed description of their
duties](persona-champions.md) (which go beyond just survey analysis).

### What About Using Personas For Quantitative Metrics?

We have found minimal value in splitting our quantitative metrics by persona.
Even when it seems like you would want to do that, there is usually another
dimension that would be better for doing analysis of the quantitative metrics.

For example, let's say you want to analyze build times for Java Backend
Developers vs JavaScript Web Developers.  Splitting the data by persona would
get you confusing overlaps—you might have some full-stack engineers who write
both Java and JavaScript. It makes the data confusing and hard to analyze.

What you would wnat to do instead in that situation is analyze the build speed
based on what language is being compiled. Then you would have actionable data
that the owners of the build tools could use to speed things up, as opposed to
a confusing mash of mixed signals.

Next: [Persona Champions](persona-champions.md)
