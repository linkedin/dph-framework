# What’s wrong with scores?

Resist the temptation to aggregate metrics into scores. Scores are problematic
for a variety of reasons.

# Issues

1. **Added Indirection** — Creating scores is tempting because it appears to
   reduce the amount of information communicated to users. But, the issue is
   that a score adds another layer of indirection. Rather than reducing the
   amount of information needed to make decisions, scores add to it.
2. **Aggregates and Weights** — Scores require additional decisions to be made
   about combining and weighting metrics. Agreeing to a standard set of weights
   distracts from the main goal of using metrics to drive priorities and
   improvements. It’s okay to let different teams prioritize different metrics.
3. **Stakeholder Buy-in** — Scores also require a lot of "buy-in" from
   stakeholders. Getting the buy-in necessary for metrics is often difficult
   enough that creating scores as "meta-metrics" isn’t worth the effort. Another
   option is to have a strong sponsor for the score. But these top-down efforts
   are rare.
4. **Expensive to Develop** — When creating a metric, lots of decisions need to
   be made about the telemetry and data pipeline. What is included or excluded
   from the metric? When does the duration start or end? Prioritize and iterate
   on these decisions before considering an aggregate score.
5. **Unactionable Changes** — Scores are less directly actionable and meaningful
   than metrics. Creating an alert on a score is error prone as one metric’s
   improvement may conceal another metric’s worsening.
6. **Increased Noise** — The changes in contributing metrics also make variance
   calculations more difficult. As fluctuations are bound to occur, the
   combination of those changes may increase the noise in the score.
7. **Missing Units** — Scores often have no units and therefore are not
   meaningful or intuitive. To say that a score went from 50 to 60 is
   meaningless without more context. Is the overall score out of 100 or 1,000?
   Is a 20% improvement typical or remarkable?
8. **Potential for Gaming** — When a set of metrics are reduced to a single
   number, there might be an incentive to "game" the system to achieve higher
   scores, potentially at the expense of other important factors.
9. **Difficulty in Comparison** — Due to inherent differences in services or
   systems, it may be difficult to meaningfully compare scores. The effort to
   improve the score in one scenario by 10% may require ten times more effort in
   another scenario for the same benefit.
