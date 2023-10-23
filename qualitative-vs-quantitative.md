# Qualitative vs Quantitative Measurements

We collect both quantitative data and qualitative data. They have different uses
and trade-offs.

## Qualitative Data

Usually qualitative data is in the form of personal opinions or sentiments about
things. It is collected by asking people questions, usually through surveys or
by interviewing people.

Qualitative data is our most "full-coverage" data. It can tell us about almost
anything that can be framed as a survey question. However, it sometimes is hard
to take direct action on, depending on how the survey questions are constructed.
Also, you usually can't survey people _frequently_ (they don't want to be
surveyed that often) which means that your data points are coming in every few
months or quarters, rather than every day. So you can't see, for example, if a
change you made yesterday caused an improvement today.

Qualitative data usually ends up being best for discovering general areas for
action, but often requires specific follow-up analysis to discover specifically
what action needs to be taken in those areas.  It is most often appropriate when
you are measuring something abstract or social (like “happiness,”
“productivity,” or “how do people feel about my product”), as opposed to
something concrete or technical (like “how many requests do I get per second” or
“how long is the median incremental build time of this specific binary?”).

That said, it is usually easier to survey/interview users than to instrument
systems for quantitative data. So when first analyzing an area, doing surveys or
interviews is usually the best way to get started. However, eventually you do
want to have quantitative data, because it's very useful when figuring out what
specific actions you need to take to fix productivity issues.

## Quantitative Data

Quantitative data is easier to take direct action on, but usually harder to
implement. It's important to know that [somebody will _use_ the
data](driving-decisions.md) before you go through the work to put numbers on a
graph.

Quantitative data is especially helpful when an engineer needs to do an
investigation that will lead to an engineering team taking direct action. For
example, "What are the slowest tests in my codebase?" An engineer asking that
question likely is about to go fix those specific tests, and then wants to see
the improvement reflected in the same metric.

It is dangerous to use quantitative methods on things that should be
qualitative. For example, **there is no general quantitative metric for
"developer productivity."**  "Productivity" is inherently a _quality_ that
you’re measuring (“how easily are people able to do their jobs?”), and there’s
no quantitative measure of it. "Code complexity" is similar---that is a quality
that is experienced by human beings; you can't measure it with a number.

## Conflicts

When the qualitative data and the quantitative data disagree, usually there is
something wrong with the quantitative data. For example, if developers all say
they are unhappy with build times, and our build time metrics all look fine, our
build time metrics are probably wrong or missing data.