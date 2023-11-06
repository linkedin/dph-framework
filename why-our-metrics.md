# Why Did We Choose Our Metrics?

This document explains why we chose the metrics described in the [example
metrics](example-metrics.md). It is here to give you an idea of the reasoning
process used to pick a metric, and why we consider some metrics good and other
metrics bad. It also contains some insights around the value (or lack thereof)
of certain common developer productivity metrics.

## Company-Wide Engineering Metrics

### Developer Build Time (DBT)

One thing that slows down [iterations](productivity-concepts.md) for software
developers is them having to wait for the build tool to finish. They make a
change and they want to see if it compiles, which is a very important and
frequent iteration. Because it happens so frequently, you can potentially save a
ton of engineering time and make engineers much more efficient by improving
build time. 

You can also fundamentally change how they work if you get build time low
enough. For example, wouldn't it be nice if you set up a system that
automatically built your code every time you saved a file, and returned instant
feedback to you about whether or not your code compiles and passes the basic
build checks?

### Post-Merge CI Duration (PMCID)

This is, to a large degree, another [iteration time](productivity-principles.md)
issue. It's less common that a developer is actively _waiting_ for a post-merge
to finish, so this isn't about [context switching](productivity-principles.md).
However, a developer may want to know that there is some problem in CI (if there
is). In particular, if the signal from the CI system comes _after_ the
developer's working hours, that means you've potentially lost a lot of
real-world time in terms of getting your feature or deployment done.

Also, just generally, just imagine the frustration and difficulty of submitting
something and only finding out that there is something wrong with the change two
or three _hours_ later (if the CI pipeline is that long), when you're already
working on something totally different. Granted, this will happen even if the CI
pipeline takes five or ten minutes, it's just not as drastically bad. If it were
just ten minutes and I _really_ wanted to wait for it to finish because I was
sending out something _really_ important that I was worried about, I could just
go get a coffee and come back. But if it takes two hours, I'm _definitely_
working on something else, or the work day has ended.

Also, long CI times mean that deployments take longer for people who do
automated continuous deployment. This means experimentation takes longer, it
takes longer to get feedback from users, etc.

This metric is not as important as Developer Build Time, because that more
directly impacts iteration time and context switching.  But we do care about
making CI faster, for the reasons specified above. There are probably also other
benefits that we don't see, which only show up in specific cases.

#### Why Not "CI Success Rate?"

The whole purpose of a CI system is that it's supposed to fail sometimes. The
problem with making this a metric is that it's [not really clear what it means
when it goes up or down](metric-principles.md). Like, what number is good?
Should it be 100% all the time? If it should be, then why does the system exist
at all?

There _is_ a good metric here that can be used called "CI Greenness" where you
measure what percentage of the time a CI build is "green," or passing. We aren't
sure this makes sense at LinkedIn, though, for a few reasons:

1. We don't actually run our builds _continuously_, but only when somebody
   merges a PR. So just one flaky test suddenly can make your "greenness" very
   bad, because you have to wait for somebody to submit a new change to fix it.
   Sometimes that might happen quickly, but it's not like there's an automated
   system that is just going to re-run the tests in a few hours anyway, to
   guarantee that flakiness has minimal impact.
2. At LinkedIn, our post-commit CI system doesn't actually _block_ developers
   from continuing to work. It just prevents deployment. (Or in the case of a
   library, prevents others from depending on the version whose CI failed.) A
   failing CI is an inconvenience, that's for sure, as you now have to
   investigate the failure, fix whatever is necessary, go through code review
   again, etc. But (in most cases at LinkedIn) other people can still submit to
   the repository, your change is still _in_ the repository (this is good and
   bad, both), and you can still continue to do work. So measuring "how long was
   CI failing for" isn't as valuable at LinkedIn as it would be in a place where
   "failing CI" means "nobody on the whole team can continue to work."

### Code Reviewer Response Time (RRT)

Code review is one of the most important quality processes at every large
software company, and LinkedIn is no exception. While there are many things
about code that can be caught and improved by machines, only human beings can
tell you if code is [easy to read, easy to understand, and easy to correctly
modify in the
future](https://www.codesimplicity.com/post/the-definition-of-simplicity/).

What you want from a code review process is that it provides continuous
_improvement_ to your code base through effective feedback from code reviewers.
This requires whatever level of strictness is necessary in order to achieve this
goal, which is different depending on who the submitter of the code is--how much
experience they have with your system, how much experience they have with the
language or tools, how long they have been programming, etc.

However, it can sometimes seem like when you are too strict, developers start to
push back about the strictness of the code review process, or they start trying
to get around it, like "let's send it to the person who always rubber stamps my
changes and never provides any feedback." This breaks the process and removes
its value for your company.

There is a secret to maintaining strictness while removing complaints: [have the
reviewers reply
faster](https://google.github.io/eng-practices/review/reviewer/speed.html) As
wild as it may sound, nearly _all_ complaints about strictness are actually
complaints about _speed_. 

Think about it this way: you submit a change, wait three days, the reviewer asks
you to make major changes. Then you submit those changes, wait three days, and
the reviewer again asks for major changes. At this point you're extremely
frustrated. "I've been waiting for a week just to submit this!" Developers in
this situation often say, "Stop being so strict!" After all, it's too late to
say, "Stop being so slow!" And the slowness has increased the tension so much
that the author can't stand it anymore, so they revolt.

On the other hand, if a developer posts a change and the reviewer sends back
comments within 30 minutes that ask for major changes, the developer might sigh
and be a little annoyed, but will do it. Then when more major changes are
requested, there might be some pushback, but at least it's all happened within
the same day or two, not after waiting for more than a week. It makes people
stop complaining about the code review process _as a whole_, and also
significantly reduces (but does not eliminate) author pushback on valid code
review comments.

#### Why not "code review volume?"

There is an [entire document that explains why any metric measuring the volume
of output of a developer is dangerous](metrics-and-performance-reviews.md).

That said, on a very large scale, PR Volume actually is an interesting metric.
Looking at this _in the aggregate_ for thousands of engineers can show us
patterns that are very interesting. Usually they tell us about things that
happened in the past more than they tell us about what we can or should _do_
about something--it's hard to take action items from it, but it can warn us
about bad situations. 

We didn't want to make this a company-wide metric because (a) it's hard to make
managerial decisions based on it (b) it's only really valid on the level of the
whole company or parts of it that have 500+ engineers (c) we were concerned it
would be mis-used by people as a measurement of engineer performance as opposed
to something we use to understand our tools, processes, or large-scale
managerial decisions.

All that said, it is possible to see PR Volume in our detailed dashboards that
track PR metrics, and it's useful _informationally_ (that is, as an interesting
input to help understand a few types of management decisions or their impact,
such as time off, large-scale changes to our engineering systems, etc.) We
include a large red disclaimer that the data should not be used for performance
management, along with a link to [our explanation about why output metrics
should not be used for individual performance ratings](scores.md). 

#### Why not "PR Creation to Merge Time?"

As noted above, code review is a quality process. When you make people focus on
the length of the whole process, you end up unintentionally driving behaviors
that you don't want. 

As an absurd example, I could make every code review fast by simply making
everybody approve them without looking at them. This metric would look beautiful
and perhaps I would be rewarded for my efforts at optimizing code review times.

As a less absurd example, let's say that a manager has instructed their team,
"Let's look into how we can make code reviews take less total time." Now imagine
that on some particular code review, a reviewer leaves a round of legitimate
comments, and the author pushes back saying, "You are making this code review
take longer," or something of that essence, and manages to talk their way out of
improvements that really should have been made, simply because of _how long_ the
review has taken in real-world days. This is a specific example, but there is a
broad general class of bad behaviors you encourage when you tell people "make
code reviews take less overall time," instead of "let's speed up how fast
individual responses come in."

When you focus on the speed of individual responses, you still get what you want
(faster code reviews), but you don't sacrifice the power of the review process
to produce high-quality code.

There actually _is_ a point at which "too many iterations" (like, too many
back-and-forth discussions between a developer and reviewer) becomes a problem
in code review, but it's super-rare that this is the problem on a team. It's
more common that people are too lax than that people are too strict. And it's
more common that people are slow to respond than that they respond too many
times. If "too many iterations" was a widespread problem at LinkedIn, we would
think about tracking a "number of code review iterations" metric just for the
duration of a project focused on solving the problem, but it's not something we
want to go to zero. We just don't want it to be absurdly high (like ten
iterations).

## Metrics for Developer Platform Team

### CI Reliability (CIR)

The CI system itself absolutely must return reliable results, or developers will
start to mistrust it. In the past, we saw some teams where nearly _every_ CI
failure was actually a failure of the CI infrastructure.

Instead of focusing on the uptime of the individual pieces, we focus on the
reliability of the system as it is _experienced by its users_. Making this the
focus of our reliability efforts dramatically improved the actual reliability of
our system, compared to previous efforts focused around only availability.

### Deployment Reliability (DR)

This has similar reasoning to CI Reliability, above.

The only point worth noting is that there are sometimes discussions about
whether the team that owns the deployment platform should be responsible for the
full _success_ of all deployments, and not just the reliability of the
deployment platform itself.  Over time, we have come to the conclusion that this
should _not_ be the responsibility of the deployment platform team, because too
many of the issues that block successful deployments are out of the hands of the
deployment platform team. 

There _are_ things that the platform team can do to make it more likely that
people have successful deployments. For example, make it easier to add
validation steps into a deployment. Make the configuration process for a
deployment simpler. But overall, the actual success of a deployment depends a
lot on the specifics of the binary being deployed and the deployment scripts
that were written by the team that owns that binary. 

If you make the deployment platform team responsible for the success of every
deployment, you tend to make them into consultants who spend too much time
debugging the failing deployments of customers and not enough time developing
new features that improve the deployment experience for the whole company.

### Number of Insights Metrics in SLO (NIMS)

We have a team whose job it is to create data pipelines and infrastructure
around developer productivity metrics. These metrics can't help anybody unless
they end up in a dashboard, and that dashboard has up-to-date data.

This metric doesn't measure the success of our dashboards. It measures the
effectiveness of our team's data infrastructure. This metric measures that we
have met the "table stakes" of being able to simply display data at all, and how
effectively we are doing that as a team. We have other metrics to measure the
impact our work has.
