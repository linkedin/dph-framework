# Data vs Insights

What is the difference between "insights" and "data?"

Data is simply raw information: numbers, graphs, survey responses, etc. A viewer
has to _analyze_ data in order to come to a conclusion or solve a mystery.

An "insight" is: **a presentation of information that solves a mystery for the
viewer**. Now, one can do this _more_ or _less_--not all insights will fully
answer _every_ question. Some might just help clarify, and the viewer has to do
the rest of the analysis to fully answer their question. 

**When you propose a system or process that provides insights, it is a good idea
to explain:**

1. **What mysteries does this solve?** 
2. **Are there mysteries it intentionally doesn't solve?**
3. **How can you assure that this system currently provides (and continues to
   provide) trustworthy insights to its users?**
4. **How will you change this system in the future if you discover a flaw in the
   metric, system, or process you’ve proposed?**
5. **How do you ensure the accuracy of the data now and in the future?**

Let's explain this a bit more, with some examples.

- [Example: Graphs](#example-graphs)
- [Example: Free-text Feedback](#example-free-text-feedback)
  - [Categorization](#categorization)
  - [Algorithmic Analysis](#algorithmic-analysis)
- [Trustworthiness of Insights](#trustworthiness-of-insights)
- [Accuracy of Data](#accuracy-of-data)

## Example: Graphs

If you have ever heard somebody say, "But what does this graph _mean_?", you
will understand the difference between data and insights. For example, let's say
you have a graph that shows the average page-load latency of all pages on
linkedin.com. This graph creates a huge mystery when it changes, for several
reasons:

1. Because it's an average, outliers can drastically affect it, meaning people
   who look at it have no idea if the spikes and dips are from outliers or from
   actual, relevant changes.
2. Because it covers so many different areas of the site, it's hard to figure
   out _who_ should even be digging into it.
3. It, by itself, provides no avenue for further investigation--you have to go
   look at a _lot_ of other data to be able to actually understand what you
   should do.

The _most_ that this graph could do is allow an [engineering
leader](audiences.md) to say, "One person should go investigate this and tell us
what is up." That's not a very impactful decision or a good use of anybody's
time. Basically, this graph, if it's all we have, _creates a problem_.

But what if, instead, we had a system that _accurately_ informed front-line
engineers and front-line managers when there was a significant difference in
median (or 90th percentile) page-load latency between one release of a server
and another? Or even better, if it could analyze changes between those two
releases and tell you specifically which change introduced the latency? That's a
much harder engineering problem, and may or may not be realistically possible.
The point, though, is that that is an _insight_. It does its best to point
specific individuals (in this case, the front-line engineers who own the system)
toward specific work.

To be clear, if you want to develop a system that provides insights into
latency, there are many levels at which you should do this and many different
stakeholders who want to know many different things. These are just two examples
to compare the difference between mystery and insight.

## Example: Free-text Feedback

One of the biggest sources of mystery is free-text answers in surveys. If there
are only a few answers that are relevant to your work, it's possible to read all
of them. But once you have thousands of free-text answers, it's hard to process
them all and make a decision based off of them. If you just give an [engineering
leader](audiences.md) a spreadsheet with 1000 free-text answers in it, you have
created a problem and a mystery for them. You have to process them _somehow_ in
order for the data to become _understandable_.

That's a reasonable way to think about the job of our team, by the way: make
data understandable.

In this specific instance, there are lots of ways to make it understandable.
Each of these leaves behind different types of mysteries. For example:

### Categorization 

One common way of understanding free-text feedback is to have a person go
through the negative comments and categorize them according to categories that
they determine while reading the comments. Then, you count up the number of
comments in each category and display them to [engineering
leadership](audiences.md) as a way to decide where to assign engineers.

However, this leaves behind mysteries like, "_What_ were the people complaining
about, specifically? What was the actual problem with the system that we need to
address?" For example, it might say that "code review" was the problem. But what
_about_ code review? If you're an engineer working on the code review system,
you need those answers in order to do effective work. Engineering leaders also
might want to know some specifics, so they understand how much work is involved
in fixing the problem, who needs to be assigned to it, etc.

This could be solved by further analysis that summarizes the free-text feedback.
Also, usually the team that works on the tool itself (the code review tool, in
our example here) wants to see all of the raw free-text comments that relate to
their tool.

### Algorithmic Analysis

There are various programmatic ways to analyze free-text feedback. You could use
a Machine Learning system to do "sentiment analysis" that attempts to determine
how people feel about various things and pull out the relevant data. You could
use an LLM to summarize the feedback.

Each of these leave behind some degree of mystery. Readers usually wonder how
accurate the analysis is. Summaries and sentiment analysis often leave out
specifics that teams need in order to fully understand the feedback.

That said, these methods can be sufficient for certain situations and for
certain [audiences](audiences.md), like when you just want to know the general
area of a problem and can accept some inaccuracy or lack of detail.

## Trustworthiness of Insights

The insights that you provide **must be _trustworthy_**. You do _not_ want to
train your users to ignore the insights that you provide. If the insights you
provide are wrong often enough, your users will learn to distrust them. Avoiding
false insights is one of the _most important_ duties of any system that
generates insights and data, because providing too much false insight for too
long can destroy all the usefulness of your system.

To be clear: _if your system frequently provides false insights to its users, it
would have been better if you hadn't made the system at all_, because you will
have spent a lot of effort to give people a system that confuses them,
frustrates them, takes up their time, and which they eventually want to abandon
and just "do it themselves."

This isn't just a one-time thing you have to think about when you first write a
system for generating insights. Your own monitoring, testing, and maintenance of
the system should assure that it continues to provide trustworthy insights to
its users throughout its life.

## Accuracy of Data

The most important attribute of **data** is that it needs to be as accurate as
reasonably possible. We often combine data from many different sources in order
to create insights. If each of these data sources are inaccurate in different,
significant ways, then it’s impossible to trust the insights we produce from
them. Inaccuracy (and compensating for it) also makes life very difficult and
complex for people doing data analysis--the data that you are providing now
creates a problem for its consumers rather than solving a problem for them.

The degree of accuracy required depends on the
[purpose](collecting-with-purpose-vs-collecting-everything.md) for which the
data will be used. If you don’t know how it’s going to be used, then you should
make the data as accurate as you can reasonably accomplish with the engineering
resources that you have.

If there is anything about your data that would not be **obvious to a casual
 viewer** (such as low accuracy in some areas) then you should publish that fact
and make it known to your users somehow. For example, if you have a system that
is accurate for large sample sizes but inaccurate for small sample sizes, it
should say so on the page that presents the data, or it should print a warning
(one that actually makes sense and explains things to the user) any time it's
displaying information about small sample sizes.

Next: [Qualitative vs Quantitative Measurements](qualitative-vs-quantitative.md)
