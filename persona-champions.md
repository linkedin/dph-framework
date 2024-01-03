# Persona Champions

There is a person or small group assigned as the "champion" for each of our
[Developer Personas](persona-champions.md). They are a _member_ of that persona.
For example, the persona champion for backend developers _is_ a backend
developer or a manager of backend developers.

Any time somebody at the company has a question about a particular persona that
isn't answered by our automated systems, the persona champion is their point of
contact. If you want some custom data analysis done about a Persona, want to
know what their requirements are, want to understand the best way to engage with
a persona, etc. then the persona champion is your best point of contact.

- [Duties of Persona Champions](#duties-of-persona-champions)
  - [Workflow Mapping](#workflow-mapping)
  - [Feedback Analysis](#feedback-analysis)
  - [Point of Contact](#point-of-contact)

## Duties of Persona Champions

### Workflow Mapping

When first creating the [Developer Personas](developer-personas.md), it is often
helpful to provide infrastructure owners with some basic information about how
that persona does work. A persona champion produces and maintains a document
that answers the questions, "What is the most common workflow that a developer
has, in this persona? What tools do they use as part of this workflow, and how
do they use them?"

For most traditional software engineers, this would include the tools they use
for:

* Design and Planning
* Source Control
* Editing Code
* Building/Compiling
* Debugging
* Dependency Management
* Testing
* Code Review
* Release / Deployment
* Experimentation
* Bug Tracking / Fixing
* Monitoring and Alerting

Each persona will have custom steps in addition to (or instead of) those. Some
personas, like data scientists, will have completely different workflow steps.

This isn't just a list of tools, but sentences that describe how those tools are
used in each "phase" of development above.

Sometimes you will find that a persona has different ways of working for each
person or team. In that case, you should document the broadest things the
persona has in common, and note that otherwise there are a lot of differences
between individuals. If there are _large_ sub-categories (essentially
"sub-personas" who have unique workflows _within_ a larger persona) you can call
out how those large sub-personas work, too. The trick is to keep the document
small enough that people can read it and you can easily maintain it in the
future, while still being useful for its readers.

These documents are useful for infrastructure owners who are engaging in new
stategic initiatives and need to understand if their plans are going to fit in
with how developers across the company work. For example, if I'm going to work
on a new web framework, does it fit in with how web developers work? Are there
any other developers who might benefit from it, at the company?

### Feedback Analysis

Persona champions are the primary people responsible for processing the feedback
from our surveys and real-time feedback systems. They get access to the raw
feedback data in order to process and categorize it into actionable
[insights](data-vs-insights.md).

After each survey, this process occurs:

1. A persona champion produces an analysis document listing out the top pain
   points for that persona. This involves categorizing the free-text feedback,
   looking at the 1 - 5 satisfaction scores produced by the survey questions,
   and doing direct follow-up interviews with developers as necessary (when we
   need more clarity on what the specific pain points are).
2. We share the analysis document with the relevant stakeholders. This always
   includes specifically notifying any team that might be involved in fixing one
   of the pain points. They should get an immediate "heads up" that their tool
   is being named as a top pain point for a persona.
3. We schedule a meeting that includes all those relevant stakeholders. The
   attendees should include people who have priority control over the work of
   the relevant infrastructure teams (i.e., the managers of the stuff named in
   the pain points). We go over the analysis document, answer questions, and
   agree on next steps. Somebody (such as a Technical Program Manager) is
   responsible for following up and making sure those next steps get executed.

It is important that this whole process happens _before_ the planning cycle of
the infrastructure teams, so that there is enough time for them to consider
developer feedback in their planning.

Persona champions also help curate the questions that go into surveys for their
persona. They get lists of questions to review, and can also propose new
questions for their persona when necessary.

### Point of Contact

We expect persona champions to be available to answer questions about a persona
from various parts of the organization. People might want more specifics about a
particular pain point noted in the feedback analysis, or they might have
questions about behavior or data not included in any of our documents. 

We expect persona champions to put in reasonable effort to answer reasonable
questions posed to them, as long as those questions will actually assist in
developer productivity if answered. If the work to answer a question would be
too extensive, it is fine for the persona champion to decline to answer it,
citing the amount of work that would be involved in getting the data.

Next: [Data vs. Insights](data-vs-insights.md)
