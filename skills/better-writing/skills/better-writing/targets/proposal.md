# Proposal, design document, idea

Covers a proposal, a design document, and a write-up of an idea that colleagues read and comment on before the work starts. It can be a shared page, a document, or a long post. Use the markup the place renders.

The readers are colleagues who know the codebase but not your reasoning, and the lead who decides whether the work goes ahead. They read it once from start to end, then come back to the parts they want to comment on.

## Shape

Use these parts in this order, and leave out a part that has nothing to say. A short idea can be only the goal, the context and the approach.

1. **Goal.** What is true when the work is done, in a few sentences or a short list. Readers judge every later part against it, so it comes before the approach.
2. **Context.** The facts that shape the design: what exists today, what you measured, what goes wrong. Only the facts the approach depends on.
3. **Approach.** Your opinion in the first person, with the reason next to each choice. Name the alternative you seriously considered and why you did not pick it, in a sentence or two. Name the trade-offs plainly: who loses what, and for how long.
4. **Work.** The parts, PRs or steps, as a list readers can comment on item by item.
5. **Not doing.** Parts you considered and would leave out, each with the reason.
6. **Order of work**, when the order matters.
7. **Open questions**, each with the person who can answer it.
8. **Later.** Only work you plan to do in a later round.

## Rules

- Explain the reasoning without selling it. A reader should see why the design is the way it is, and be able to disagree with one choice and keep the rest. No superlatives and no promised gains you did not measure.
- It is a proposal until people agree. Write "I would" or "I propose", not "we will", and leave out a "Decisions" section. A design document records a decision only when it was made, with who made it and when.
- Say how sure you are about each part. When you are unsure about one, say why and say that it can be dropped. Mark that the same way everywhere, for example with a "not sure we need it" tag or a muted color.
- Do not tell readers how to review or comment.
- Each item in the work list stands on its own: what it does, why, what it changes for others, and what it waits for. A reader who comments on one item does not need the rest.
- When an item bundles several parts, list the parts, so a reader can drop one and keep the others.
- Define page-local IDs once, near the top, and use them the same way everywhere. They are the only invented names allowed, because readers use them in comments.
- Later is only for planned work. A part you would not do goes under "Not doing", with its reason.
- Say what the proposal is based on: "based on the diff and git history, nothing was built or run".
- A small idea fits on one screen. A plan with many items can be long, so give it an index.

## Example

A short idea write-up:

```markdown
# Retry failed exports with a back-off

## Goal

An export that keeps failing stops filling the log and the job queue, and an export that fails once still retries quickly.

## Context

`ExportScheduler` retries a failed export every 10 minutes, with no limit. Last week 3 exports failed for 2 days because a share was full, which added 860 retries and 2,500 ERROR lines to the log.

## Proposed approach

I would double the retry interval after each failure, from 10 minutes up to 5 hours, and reset it after a success. An export that fails once then still retries after 10 minutes. I also considered a maximum number of retries, but then an export never runs again after a long outage until someone restarts it.

After a long outage, an export can wait up to 5 hours after the share is fixed. I think that is acceptable, because the exports run once a day.

## Work

- `ExportScheduler` keeps a failure count per export and picks the interval from it.
- The interval limits come from the export settings, so a customer can change them. I'm not sure we need this part, because nobody has asked for it, so it can be dropped.

## Open questions

- Should hourly exports have a lower limit than 5 hours? Product owner.
```
