# PR comment

Covers a review comment on a diff line, a reply in a PR thread, and the summary review comment. A review skill may set its own structure, such as decision threads or a lens table. Keep that structure and apply these rules to the prose in it. Markdown renders.

The reader is the PR author, who knows this code better than you.

## Review comment on a line

- Post one only when the author must consider or act on something. Positive notes go in the summary comment.
- One issue per thread, on the line where the problem is.
- Write it as one flowing explanation: what the code does, what goes wrong as a result, how much that matters, then what we could do or the open question. Often three to five sentences.
- Group related cases in one sentence ("fails when the helper is not on PATH, when `azcopy` cannot list the container, or when `az` cannot get a token") instead of one sentence per case.
- Show the failure with a concrete case, the state and the effect: "A server with 4 GB free used to save small files. Now it refuses all of them." Not "this may cause issues".
- Weigh it. Say which cases are realistic and which are unlikely, and say when a case is not worth handling and why ("those would break the pipeline in more places than this one").
- A suggestion is optional. When you know the fix, propose it as "We could ..." or with a code snippet. When you see the problem but not the right direction, ask the question in plain words: "Do you know if ...?" Say what you checked and what you could not decide, so the author can answer from what they know. Do not invent a fix to fill the slot.
- If you are not sure it is a bug at all, say so ("I think", "could") and say why you ask.
- More than two short paragraphs usually means two comments, or a point for the summary.

## Reply in a thread

Answer first, in one line where you can: "Fixed in `<commit>`: <what changed>." or "Not changed: <reason>." A short, informal reply is fine: "yeah true, good to be aware at least".

A reply that makes a new point, such as a suggestion or an objection, follows the length rules for a review comment on a line.

## Summary review comment

The verdict first (approve, wait for author, reject) with a one-sentence reason. Then the threads that block. A short, honest overall impression is fine: "Overall big improvement!".

## Examples

The user's rewrite of a comment on `scripts/ci/remote-cache.ts`, which weighs three failure modes (the last sentence fills in the suggestion they left open):

> `setup` fails when the helper is not on PATH, when `azcopy` cannot list the container, or when `az` cannot get a token. The job then fails, and we get a failing build where we could still do a cold build without the cache. The helper not being on PATH is a reasonable failure mode, as we have to build and provision it ourselves. The other two might not be worth handling, because they point to larger problems that would fail the pipeline in more places than this one. We could log a warning when the helper is missing and run without the remote cache.

The user's own general comment on a PR:

> Overall big improvement! For some i would say the start title is better than after the answer. E.g. for "Why are EU checkouts slow --> Payment provider adds latency". The user probably looks for EU checkouts in the title if they want to find that conversation again, but after the answer it is gone. Maybe have the agent check the original question for unique discerning identifiers and instruct not to remove those from the title.
