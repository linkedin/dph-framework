# Example Metrics

Here are some actual metrics we have used inside of LinkedIn, along with their
complete definitions. We are not holding these up as the "right" metrics to
use--only as examples of how to precisely define a metric. There is also another
document that explains [why we chose each metric](why-our-metrics.md), if you'd
like to get some insight into the thinking process behind each one.

These are not all the metrics we use internally; only a subset that we think are
good examples for showing how to define metrics, and which we have found useful.

We give each metric an abbreviation that we can use to refer to it. For example,
internally, when we talk about "Developer Build Time," most people familiar with
the metric just call it "DBT."

Every metric gets a "TL;DR" summary, which most casual readers appreciate.

These definitions are written so that implementers can implement them, but
_also_ so that people who have questions about "What specifically is this
actually measuring?" can have a place to get that question answered.

## Company-Wide Engineering Metrics

These are some examples of metrics we measure for the whole company.

### Developer Build Time (DBT)

**TL;DR: How much time developers spend waiting for their build tool to finish
its work.**

The intention of this metric is to measure the amount of time that human beings
spend waiting for their build tool to complete. This is measured as the
wall-clock time from when the build tool starts a "build" to when it completes.

This measures all human-triggered builds. At present, this includes all
human-triggered builds with the following tools:

- Gradle
- Bazel
- Ember 
- Xcode 

This duration is measured and reported in _seconds_.

We count this only for builds invoked by human beings, that we reasonably assume
they are waiting on. To be clear, this means we exclude all builds run on the CI
infrastructure.

We report this as P50 (median) and P90, so we have “DBT P50” and “DBT P90.”

### Post-Merge CI Duraction (PMCID)

**TL;DR: How long is it between when I say I want to submit a change and when
its post-merge CI job fully completes?**

The time it takes for each PR merge to get through CI, during post-commit.
Counted whether the CI job passes or fails. 

The start point is when the user expresses the intent to merge a PR, and the end
point is when the CI job delivers its final signal (passing or failing) to the
developer who authored the PR. 

Reported in minutes, with one decimal place. 

We report the P50 and P90 of this, so we have “PMCID P50” and “PMCID P90.”

### CI Determinism (CID)

**TL;DR: Test flakiness (just the inverse, so it’s a number that’s good when it
goes up).**

Each codebase at LinkedIn has a CI job that blocks merges if it fails. Each
week, at some time during the week while CI machines are otherwise idle, we run
each of these CI jobs many times at the same version of the repository (keeping
everything in the environment identical between runs, as much as possible). We
are looking to see if any of the runs returns a different result from the others
(passes when the others fail, or fails when the others pass).

The system that runs these jobs is called **CID**.

Each CI job gets a **Determinism Score**, which is a percentage. The
**Denominator** is the total number of builds run for that CI job by CID during
the week. The **Numerator** is the number of times the CI job passed. So for
example, let's say we run the CI job 10 times, 3 of them fail, and 7 of them
pass. The score would be 7/10 (70%).

However, if _all_ runs of a job fail, then its Determinism Score is 100%, and
its Numerator should be set equal to its Denominator.

When we aggregate this metric (for example, to show a Determinism score for a
whole team that owns multiple MPs) we average all the Determinism Scores to get
an overall Determinism Score. Taking the average means that codebases that run
less frequently but are still flaky have their flakiness equally represented in
the metric as codebases that are run frequently.

Note that this is intended to only count CI jobs that block deployments or
library publishing. It’s not intended to count flakiness in other things that
might coincidentally run on the CI infrastructure.

### Code Reviewer Response Time (RRT)

**TL;DR: How quickly do reviewers respond to each update from a developer,
during a code review?**

One of the most important qualities of any code review process is that
[reviewers respond _quickly_](why-our-metrics.md). Often, [any complaints about
the code review process (such as complaints about strictness) vanish when you
just make it fast
enough](https://google.github.io/eng-practices/review/reviewer/speed.html). This
metric measures how quickly reviewers respond to each update that a developer
posts.

#### Definitions

**Author**: The person who wrote the code that is being reviewed. If there are
multiple contributors, all of them count as an Author.

**Reviewer**: A person listed as an assigned reviewer on a PR.

**Code Owner**: A person listed in the ACL files of a code repository. A person
who has the power to approve changes to at least one of the files in a PR.

**Request**: When a Reviewer gets a notification that an Author has taken some
action, and now the Author is blocked while they are waiting for a response.
Usually this means an Author has pushed a set of changes to the repository and
the Reviewer has been sent a notification to review those changes. (Note: The
Request Time is tracked as when a notification was sent, not when the changes
were pushed. If a PR has no assigned Reviewer and changes are pushed, the
Request Time only is tracked when the Reviewer gets assigned to the PR.)

**Response**: The first time after a Request that a Reviewer or Code Owner
responds on the PR and sends that response to the author. This could be a
comment in the conversation, a comment on a line of code, or even just an
approval with no comments.

#### Metric

Measure the [business hours](metric-principles.md) between each Request and
Response. Note that in the process of a code review, there are many Requests and
Responses. We count this metric only once for each Request within that code
review.

For example, imagine this sequence of events:

1. 10:00: Author Alice posts a new change and requests review.
2. 10:20: Reviewer Ravi posts a comment.
3. 10:25: Reviewer Rob posts a comment.
4. 10:45: Author Alice posts an updated set of changes in response to the
   Reviewers' comments.
5. 10:55: Reviewer Rob approves the PR with no comments.

That creates two events. The first is 20 minutes long (Step 1 to Step 2), and
the second is 10 minutes long. (Step 4 to Step 5) The response at 10:25 (Step 3)
is ignored and doesn't have anything to do with this metric.

We then take every single event like this and take the overall P50 (median) and
P90 of them, so we have “RRT P50” and “RRT P90” that we report.

This metric is reported in [business hours](metric-principles.md) as the unit,
with one decimal place.

When displaying this metric, show it to the managers of the _reviewers_, not the
managers of the _authors_. That is, show people how long they took to review
code, not how long they waited for a review. We have found it to be more
actionable for managers, this way.

## Metrics for the Developer Platform Team

These are a few example metrics that the Developer Platform team uses to measure
their success. Unlike the company-wide metrics, these metrics tend to be things
that the developer platform team has more direct control over and that more
accurately represent the specific work they do.

We would like to reiterate: we have many more metrics for our Developer Platform
team besides these. These are just a few examples to show how one might define
metrics for an individual team, as opposed to the whole company.

### CI Reliability (CIR)

**TL;DR: How often does CI fail because of a problem with CI infrastructure?**

How often do users experience a CI failure that is not due to an error they
made, but instead was due to a breakage or bug in our infrastructure?

The only failures that are counted are infrastructure failures. So if a job
succeeds or fails only due to a user error (like a test failure--something the
system is supposed to do) then that doesn’t count as a failure. Any failure that
we don’t know is a user failure is assumed to be an infrastructure failure.

Reported as the success percentage. (That is, a number that is good when it goes
up.)

### Deployment Reliability (DR)

**TL;DR: How often do deployments fail because of a problem with the deployment
infrastructure?**

How often do users experience a deployment failure that is not due to an error
they made, but instead was due to a breakage or bug in our infrastructure?

Measured as how often a deployment job experiences no deployment infrastructure
failures. A “successful” deployment job is one where one version of one
deployable has been deployed to all machines (or locations) it was intended to
be deployed to per its deployment configuration. However, we only count failures
of the deployment infrastructure as failures, for this particular metric.

Deployments can partially fail. For example, one machine might deploy
successfully while another fails due to infrastructure-related reasons. In our
deployment infrastructure, individual teams can define what constitutes a
“successful” deployment in terms of the percentage of machines that successfully
deployed. We count a deployment as successful if it deployed to that percentage
of machines.

Infrastructure failures do include machine-based failures, like bad hosts that
won’t accept deployments. They also include failures of the config
infrastructure (but not config syntax errors or things like that). (This is not
a complete list of what is included--we just note these specific things that are
included so there isn’t confusion about those specific things.) 

Reported as the success percentage. (That is, a number that is good when it goes
up.)

### Number of Insights Metrics in SLO (NIMS)

**TL;DR: How many metrics are presented in our central developer productivity
dashboard, and are they updating regularly on time every day?**

To calculate this metric, first we count up all the metrics in our central
developer productivity dashboard that have been fully implemented. "Implemented"
means, for each metric:

1. We have an automated pipeline that does not require human interaction, which
   dumps data to some standard data store.
2. The data is processed by data pipelines to create metrics which are then
   displayed in our central developer productivity dashboard.
3. The metric displayed in our dashboard has passed User Acceptance Testing
   (UAT) and is viewable in production.

We count the number of metrics in our central dashboard, not the number of
pipelines. One pipeline might produce multiple metrics.

The current SLO for our metrics is: each workflow for the metrics will compute
data that is no older than **30 hours**. The definition of “compute” here is
“calculate and provide in a format that is consumed by the dashboard.”

For every metric where the latency is within SLO, we count "1" for this metric.

When displaying this metric for a time period longer than a day, we average out
the latency of each update over the time period we want to measure. For example,
if we are measuring this for a quarter, we average them out over the whole
quarter. By "each update" we mean every time the pipeline updated itself such
that the dashboard would show an updated number. By "latency" we mean the time
between each update, or the time between the last update and present time. 