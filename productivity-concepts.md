# Productivity Concepts for Software Developers

There are some common concepts used when discussing the productivity of software
developers. These concepts aren't specific to designing metrics, but they
frequently come up when we think about which metrics to choose.

- [Iteration Time (aka Cycle Time)](#iteration-time-aka-cycle-time)
- [Context Switching](#context-switching)

## Iteration Time (aka Cycle Time)

One of the most important things to optimize about software engineering is
"iteration time," which is the time it takes for an engineer to make an
observation, decide what to do about that observation, and act on it. There are
small iterations, like when a person is coding, they might write a line of code,
see the IDE give it a squiggly red underline, and fix their typo. And there are
huge iterations, like the time between having an idea for a whole product and
then finally releasing that product to its users, getting feedback, and making
improvements to the product. There are many types and sizes of iterations, like
doing a build and seeing if your code compiles, posting a change and waiting for
a code review comment, deploying an experiment and analyzing feedback from
users, etc.

Sometimes, we don’t have a set expectation for how many iterations a process
should take, but we know that if we speed up the iterations, the process as a
whole will get faster. It’s a safe general assumption to make in almost all
cases. 

Also, there are times when you fundamentally change the nature of the work by
reducing iteration time. For example, if it takes 2 seconds to run all my tests,
I can run them every time I save a file. But if it takes 10 minutes, I might not
even run them before submitting my code for review. In particular, work can
dramatically change when iterations become short enough to eliminate context
switching, as described below. 

## Context Switching

Developers will "context switch" to another activity if they have to wait a
certain amoun tof time for something. For example, they might go read their
email or work on something else if they have to wait longer than 30 - 60 seconds
for a build to complete. The specific time depends on various factors, such as a
person's expectations for how long the task _should_ take, how the task informs
the developer of its progress, etc.

When you interrupt a developer for long enough, they could take up to 10 - 15
minutes to mentally "reload" the "context" that they had for the change they
were working on. Basically, it can take some time to figure out what you were
working on, what you were thinking about it, and what you intended to do.

So if you combine those two, there’s a chance that every time you make somebody
wait longer than a certain amount (let's say 30 seconds, on average), you
actually could lose fifteen minutes of their time. Now, this isn’t an absolute
thing--you might only lose two or three minutes for a 30-second wait, but you
might lose 5 - 10 minutes for a 3-minute wait.

Also, sometimes important context is entirely lost from the developer’s mind
when you make them context switch, especially when the context switch comes from
a sudden interruption (like having some service go down that they depend on for
development). They come back to what they are doing and have forgotten something
important, leading to bugs or missed opportunities in your actual production
systems.

So it’s important to avoid making developers context switch.

Next: [Example Metrics](example-metrics.md)