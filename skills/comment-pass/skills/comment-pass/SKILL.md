---
name: comment-pass
description: >-
  Clean up the code comments and docs a branch adds, then commit the fixes. Use when asked
  to check, clean up or condense the comments and docs on a branch, such as before a PR
  goes to review. Not for reviewing behaviour or comments the branch did not add.
---

# Comment pass

Scan the comments and documentation a branch adds, fix what is wrong, and commit. The scan
is delegated to a cheap model. The fixes and the commit happen in the main session, without
asking first, because every change is small and easy to revert.

## 1. Scope

- Default: the lines the current branch adds compared with its base branch
  (`git diff <base>...HEAD`, plus uncommitted changes). Take the base from the open pull
  request, else the branch's upstream fork point, else the default branch.
- An argument narrows or replaces this: a path, a commit range, or a pull request.
- In scope: code comments, doc comments, in-repo documentation (decision records, READMEs,
  guides), and log and error texts the branch adds.
- Out of scope: comments and docs the branch did not add or change, and code behaviour.

Stop and say so when the branch adds no comments or documentation.

## 2. Scan with Sonnet

Start one read-only subagent on Sonnet. For a large diff, start one per area (a module, the
docs folder) so each file is read once. The subagent only reports. It does not edit, commit
or post.

Give it the repo path, the diff command, and this checklist:

1. **Accuracy.** Does the comment say what the code next to it does? Flag statements that
   are wrong, outdated, or promise more than the code does. Read the surrounding code.
2. **One line.** A comment is one line. Flag multi-line blocks and give a one-line version.
3. **Self-contained.** A reader with no knowledge of the change must understand it. Flag
   wording that narrates the change ("now", "no longer", "previously", "we changed"),
   ticket or pull request numbers, and names of people or customers.
4. **No dead pointers.** Flag references a reader of the code cannot act on: a patch
   file, a chat thread, a spike, an unnamed "earlier design". The fact goes in the
   comment itself or is left out.
5. **Right place.** Flag a comment that documents a different function or member than the
   one it sits on, and one that only restates the code.
6. **Documentation.** Contradictions inside the document, claims that disagree with the
   code, figures with nothing to back them, references to things the document never
   explains, typos.
7. **Log and error texts.** Clear, correct, plain language. Does the text say what the
   number is and what the reader should do?

Add the project's own comment and documentation rules to the checklist when it has them
(contributor guide, agent instructions, linter configuration). They win over the defaults
above. Also tell the subagent what is already known or decided, so it does not report it
again.

Ask for a list, most important first: `file:line`, the quoted text, what is wrong, and a
suggested replacement. "None" for a category with nothing to report.

## 3. Check each finding

The scan is cheap and makes mistakes. Before changing anything, read the code or document
each finding points at and sort it:

- **Fix:** the finding holds and there is one obvious fix.
- **Drop:** the finding is wrong, or the fix would break a project rule or a check. Example:
  a documentation linter only accepts certain values in a field, and the suggestion uses
  another one.
- **Leave for the user:** the right text depends on a design choice that is still open, or
  the fix would change behaviour.

## 4. Fix

Apply the fixes directly:

- Condense a multi-line comment to one line. Keep the reason, drop the mechanics the code
  already shows. When a block documents several things, give each its own one-line comment
  where it belongs.
- Correct an inaccurate comment from the code, not from the suggestion. When you cannot
  tell which of the two is wrong, leave it for the user.
- Remove a dead pointer. Keep a file name where the file is used right there, such as a
  patch in a build script's patch list.
- In documentation, replace an undefined reference by what was done and found, and replace
  a claim that has no backing by one that has, citing the test or measurement.
- Before changing a log or error text, search the repo for anything that matches on the old
  text (tests, alert rules, scripts) and update it with the text.
- Do not add comments. This pass shortens, corrects and removes.

Run the checks that cover the touched files when they are cheap: the documentation linter,
the formatter. Leave formatting to a pre-commit hook when the repo has one.

## 5. Commit

Commit without asking, following the repo's commit convention:

- Comments and documentation only: one docs commit, such as
  `docs(<scope>): shorten and correct the comments on <subject>`.
- A changed log or error text is not documentation. Put it in its own commit of the type
  the convention gives for it, such as `chore` or `fix`.
- Keep unrelated uncommitted work out: stage only the files this pass touched. When one of
  those files also holds unrelated uncommitted changes, do not commit it. Report it.
- Do not push unless the user asked for that.

## 6. Report

Tell the user, briefly:

- what was fixed, grouped by kind, with the commit;
- what was dropped and why, in a line each;
- what is left for them to decide, with the options.
