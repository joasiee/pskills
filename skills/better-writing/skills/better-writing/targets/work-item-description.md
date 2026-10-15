# Work item description

Covers the description of a Bug or PBI, repro steps, and acceptance criteria. When another skill or a template owns the title and the fields, follow it. Otherwise a Bug title states the problem, a PBI title the goal, and neither gets a Conventional Commits prefix.

The readers are whoever picks the item up months later, the tester, and the product owner who prioritizes it. Write so the item works without you.

## Bug

On a Bug the text goes in Repro Steps (`Microsoft.VSTS.TCM.ReproSteps`). Use these parts in this order, and leave out a part that has nothing to say:

- **Symptom.** What the user or the log shows, with the exact error or log text, where, and on which version. Readers find the item by searching for that text.
- **Impact.** Who is hit and how badly, with numbers: customers, frequency, duration.
- **Repro.** Numbered steps from a clean state, one action each. If you did not reproduce it, say where it was seen.
- **Cause.** Only when verified, with the file and function. Otherwise label it "Suspected cause".
- **Fix direction.** What should change, not the diff. With several options, say which one you tested.
- **Not in scope.** Only what a reader would otherwise expect to be covered.
- **How to verify.** What a tester checks after the fix, and where.

## PBI

- **Goal.** What a user or colleague can do when this is done, and why it matters.
- **Acceptance.** Checks a tester can pass or fail. "A failed upload shows the retry banner" decides something. "Handle errors well" does not.
- **Not in scope**, and **open questions** with the person who answers each one.

## Rules

- Each part starts with its bold label and a period, as above. Here, label-led paragraphs are fine.
- Keep the measurements and log lines that decide the fix. Leave out how you found them.
- Mark what you measured and what you assume: "measured on kind", "not tested".
- The field stores HTML. Match the existing items: `<p>`, `<b>`, `<ul>`, `<ol>`, `<code>`.
- A typical bug fits on one screen. Go longer only for measurements that decide the fix.
