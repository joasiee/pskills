---
name: better-writing
description: >-
  Writing style for any text that leaves this session for other people: PR descriptions,
  PR review comments and thread replies, work item (Bug/PBI) descriptions, repro steps and
  acceptance criteria, work item comments, commit messages, team announcements, chat
  messages drafted for colleagues, and customer-facing text such as emails, support
  replies, incident updates and postmortems.
  Use it whenever you draft, post, or edit such text, also when another skill or workflow
  produces it, and even when nobody asks for a style. Applies a per-target style on top of
  a shared plain-English baseline. Not for replies to the user in this chat, code comments,
  or in-repo docs.
---

# Better writing

Text that leaves this session is read by someone who never saw the session. Usually that is a colleague. For emails, support replies and incident reports it is a customer. Write for that person.

## Workflow

1. Name the target and read its file in `targets/`. No matching target: use the baseline alone.
2. Draft with the baseline below, then apply the target file. Where they conflict, the target file wins.
3. Run the self-check before the text leaves the session.

| Target | File |
|---|---|
| PR description | `targets/pr-description.md` |
| PR review comment, reply in a PR thread | `targets/pr-comment.md` |
| Work item description, repro steps, acceptance criteria | `targets/work-item-description.md` |
| Work item comment | `targets/work-item-comment.md` |
| Customer-facing text: email, support reply, incident update, postmortem | `targets/customer-message.md` |
| Commit message, PR title | `targets/commit-message.md` |
| Announcement in a chat channel (usually company-wide) | `targets/announcement.md` |
| Direct chat message to a colleague | `targets/chat-message.md` |

## Baseline

### Voice

- Concise and to the point. Say each thing once.
- Write like a colleague explaining it at their desk, not like a report. Friendly and a bit tentative is fine.
- Match the wording to how sure you are. Use "I think", "could", "might" or "maybe" for what you reasoned out but did not see happen: "I think a run that stopped on a question could ring "investigation completed"." Use one such word per claim, not several.
- No politeness padding: no thanks, apology, or filler softener ("just", "I was wondering whether we might perhaps"). A plain "please" in front of a real ask is fine.
- A short, honest verdict is fine where it helps the reader: "Overall big improvement!". No praise sprinkled around the point.
- Name problems and trade-offs plainly: "this breaks format on save", "that is not ideal".
- Give the problem its weight. Say how likely each case is and how bad, separate the realistic case from the unlikely ones, and say when something is not worth handling.
- Own an opinion in the first person, with the reason: "I think the git hook is the better option, because it also formats code Claude writes."

### The reader was not here

- Open with the point. Then give the premise the reader is missing: what you saw, where, and why it matters. One or two sentences, not a run-up.
- Use the codebase's names: classes, functions, settings, work item titles. Drop every name this session invented ("the stale-handle race", "option B", "phase 2", "the fix from earlier"). If a concept has no name in the code, describe it.
- Write for what this reader knows. Explain an abbreviation or domain term the reader may not know, such as an internal record type for a product owner. A product owner or tester needs what it means for customers and planning, not the mechanism.
- No session residue: "as discussed", "as requested", "per your instructions", "after investigating".
- Shorter and clearer, never shorter and blunter. Cut words, not context.

### Plain English (ASD-STE100, light)

- Let the text flow. Join facts that belong together with "and", "so", "but", "when" or "then", instead of a row of short factual sentences. Keep most sentences under about 25 words.
- Active voice with a named actor: "`JobQueue` drops the job", not "the job is dropped".
- Simple tenses. Keep the present perfect only when it carries current state.
- Plain verbs, no phrasal verbs: "start", not "spin up". "Use", not "leverage" or "utilize".
- One term per concept. Never rotate synonyms for the same thing.
- Keep articles and verbs. No arrows, symbol-speak, or verbless fragments in prose.
- A number beats an adjective: "3 of 140 keys", not "some keys".

### Truth

- State only what you checked. Label the rest: "I expect", "not verified".
- Keep a hedge that carries real doubt, one per claim. Cut stacked hedges.
- Never turn "may have failed" into "failed", or add a cause the evidence does not show.

### Cut on sight

- AI vocabulary: delve, crucial, pivotal, robust, seamless, comprehensive, enhance, leverage, showcase, underscore, foster, landscape, testament, intricate, additionally.
- Abstract metaphor nouns: surface (as in "API surface"), vector, substrate, wedge, north star, harness, primitive.
- "Serves as", "stands as", "acts as", "features", "boasts". Write "is" or "has".
- Antithesis: "not X, but Y", "this isn't about X, it's about Y". State the positive claim.
- Groups of three made for rhythm. Use the natural count.
- Trailing -ing tails: ", ensuring...", ", highlighting...", ", making it easier to...".
- Filler: "in order to", "it's important to note", "note that", "essentially", "basically".
- Vague attribution: "some argue", "best practice says". Name the source or own the opinion.
- Recaps and closing meaning-sentences ("Overall...", "This makes the flow more robust"). End on the last fact.
- Chatbot tone: "Great question", "Good catch!", "You're absolutely right", "Hope this helps", "Let me know if...".
- Personified code ("the parser wants", "the plan holds it"). Name the code that acts.

### Formatting

- No em dashes or en dashes. No semicolons. Use a period or a comma.
- Colons only before a list, an example, or code.
- Bold only for the one thing the reader must not miss. No "**Label:** sentence" bullets.
- Sentence case headings. No emoji. Straight quotes.
- Identifiers, paths, and error text in backticks.
- Markdown only where the target renders it. The target file says which.

## Self-check

1. Could the reader act on it without having seen this session? Every noun is in the code or explained, at this reader's level.
2. Read it aloud. Rewrite what you would not say to this reader in person, including a row of clipped facts that does not flow.
3. Does the reader know how much this matters? For a colleague, likelihood and impact are stated. For a customer, the effect on their work is stated and nothing internal is shared. Claims are no surer than the evidence.
4. Scan for the "Cut on sight" list and the formatting rules.
5. Delete the last sentence. If nothing is lost, leave it deleted.

## Language

Write in English, even when the user briefs you in Dutch. Use Dutch only when you answer a thread that is in Dutch.
