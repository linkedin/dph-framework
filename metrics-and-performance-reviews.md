# Metrics and Performance Reviews

It is dangerous to use numbers representing the _volume of output_ of a software
engineer to determine their job performance—numbers like "lines of code
produced," "number of changes submitted to the repository," "numbers of bugs
fixed," etc. This doc explains why and offers some alternative suggestions of
how to understand and manage the performance of software engineers.

- [Why Is This Dangerous?](#why-is-this-dangerous)
  - [Perverse Incentives](#perverse-incentives)
  - [Doesn’t Actually Do What You Want](#doesnt-actually-do-what-you-want)
  - [Clouding the Metrics](#clouding-the-metrics)
- [What Do You Do Instead?](#what-do-you-do-instead)
  - [Examples of Good Metrics](#examples-of-good-metrics)

## Why Is This Dangerous?

### Perverse Incentives

When you measure the output of a software engineer instead of their impact, you
create perverse incentives for software engineers to behave in ways that
ultimately damage your business.

Let’s say that you see that a software engineer has submitted very few pieces of
code to the repository in this quarter. If you use this to manage their
performance, you might say, "Let’s figure out how you can submit more code,"
Sometimes, this will result in good behaviors—perhaps they were spending too
long on one large change that they will now submit as three smaller changes,
making everybody happier. Nice.

However, there’s absolutely no guarantee that this _will_ result in good
behavior, because all you’re measuring is this absolute number that doesn’t
actually tie back to the business impact that the developer is having. The same
person, at a different time, could look at a change they have that really
_should_ be submitted all at once, and split it into 100 different changes just
because it will cause their numbers to go up. That causes a ton of unnecessary
work for them and their code reviewer, but it looks great on their performance
review. Then they may even sit back and delay the rest of their work until
_next_ quarter because they "already got their change count up." This may sound
remarkable but is actually very rational behavior for a person whose primary
concern is their performance review and knows specifically that this metric is
being used as an important factor in that review.

### Doesn’t Actually Do What You Want

It’s assumed that we are managing the performance of software engineers because
we have some goal as a business, and software engineers are here to contribute
to that goal. So we are managing their performance to make sure that everybody
contributes to that goal as much as possible and that the business succeeds.

The goal of the business is not "to write code." Thus, when you measure how
_much_ code somebody is writing, you don’t actually get a sense of how much they
are contributing to the business. Sometimes, you do get a general idea—person X
writes 100 changes a month and person Y writes 4. But honestly, that’s not even
meaningful. What if those 4 changes required a ton of background research and
made the company a million dollars, while those 100 changes were all sloppily
done and cost the company a million dollars in lost productivity and lost users?

The same happens with measuring "how many bugs got fixed." It’s possible that
somebody spent a lot of time fixing one bug that was very valuable, and somebody
else spent the same time fixing 10 bugs that didn’t actually matter at all, but
were easy to handle. The point here isn’t how much time got spent—it’s about
how valuable the work ended up being. If you measure _how much effort_ people
are putting into things, you will get an organization whose focus is on _making
things more difficult_ so that they can show you _how hard it was to solve their
problems_.

### Clouding the Metrics

All of the metrics that we have around our developer tools, such as volume of
code reviews, speed of code reviews, speed of builds, etc. have definite
purposes that have nothing to do with individual performance reviews. Taken in
aggregate across a large number of developers, these numbers show trends that
allow business leaders and tool developers to make intelligent decisions about
how best to serve the company. When you look at a group of 1000 developers, the
differences between "I worked on one important thing for 100 hours" and "I
worked on 100 unimportant things for 1 hour each" all even out and fade away,
because you’re looking at such a large sample. So you can actually make
intelligent statements and analysis about what’s happening, at that scale. If
the volume of code reviews drops _for the whole company_ for a significant
period of time, that’s something we need to investigate.

However, if you make people behave in unusual ways because their _individual
performance_ is being measured by the same metrics, then suddenly it’s hard for
business leaders to know if the numbers they are looking at are even _valid_.
How do we know if code review volume is going up for some good reason related to
our tooling improvements, or just because suddenly everybody started behaving in
some weird way due to their performance being measured on these numbers? Maybe
code review times went down on Team A because their performance was measured on
that, so they all started rubber-stamping all code reviews and not really doing
code review. But then some executive comes along and says, "Hey, Team A has much
lower code review times than our other teams, can we find out what they are
doing and bring that practice to other teams?" Obviously, in this situation what
would really happen is that we would find out what Team A was doing and would
correct it. But ideally this confusion and investigation from leadership would
never have to happen in the first place, because nobody should be measuring the
performance of individual software engineers based on such a metric.

## What Do You Do Instead?

There are two types of measurements that you can use, qualitative (subjective)
measurements, like surveys and talking with your reports, and quantitative
(objective) measurements, like numbers on graphs. This document is mostly about
the quantitative side of things, because we’ve found a particular problem with
that. We won’t cover the qualitative aspects here.

If you really want quantitative measurements for your team or developers, the
best thing to do is to figure out the goal of the projects that they are working
on, and determine a metric that measures the success of that goal. This will be
different for every team, because every team works on something different.

The truth is, "programming" is a _skill_, not a _job._ We wouldn’t measure the
_performance of a skill_ to understand the _success of a job._ Let me give an
analogy. Let’s say you are a carpenter. What’s the metric of a carpenter? You
can think about that for a second, but I’ll tell you, you won’t come up with a
good answer, because it’s a fundamentally bad question. I have told you that a
person has a _skill_ (carpentry) but I haven’t actually told you what their
_job_ is. If their job is that they own a furniture shop that produces custom
furniture, then the success there is probably measured by "furniture delivered"
and "income produced greater than expenses." But what if they are a carpenter on
a construction job site? Then their success is probably measured by "projects
that are complete and have passed inspection." As you can see, a skill is hard
to measure, but a _job_ is something that you can actually understand.

So to measure the success of a programmer, you have to understand what their job
is. Hopefully, it’s tied to some purpose that your team has, which is part of
accomplishing the larger purpose of the whole company somehow. That purpose
results in some product, that product has some effect, and you can measure
something about that product or that effect.

Yes, sometimes it’s hard to tie that back to an individual software engineer.
That’s where your individual judgment, understanding, communication, and skills
as a manager come into play. It’s up to you to understand the work that’s
actually being done and how that work affected the metrics you’ve defined.

And yes, it’s also possible to design success metrics for your work that are
hard to understand, difficult to take action on, or that don’t really convince
anybody. There is a [whole system of designing and using
metrics](goals-signals-metrics.md) that can help get around those problems.

### Examples of Good Metrics

These are just examples. There could be as many metrics in the world as there
are projects.

**User-Facing Project:** Usually, your work is intended to impact some business
metric. For example, maybe you’re trying to improve user engagement. You
can do an experiment to prove how much your work affects that business metric,
and then use that impact as the metric for your work, as long as you can see
that same impact after you actually release the new feature. Bugs could be
thought of as impacting some metric negatively, even if it’s just user
sentiment, and thus one can figure out a metric for bug fixing that way.

**Refactoring Projects:** Let’s say that you have an engineer who has to
refactor 100 files across 25 different codebases. You could measure how many of
those refactorings are done. You could count it by file, by codebase, or by
whatever makes sense. You could also get qualitative feedback from developers
about how much easier the code was to use or read afterward. Some refactoring
projects improve reliability or other metrics, and can be tracked that way. It
just depends on what the intent is behind the project.

Next: [Productivity Concepts for Software Developers](productivity-concepts.md)