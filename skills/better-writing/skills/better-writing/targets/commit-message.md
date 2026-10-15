# Commit message

Covers commit messages and PR titles. PRs are squash-merged, so the PR title becomes the commit that lands.

- Format: Conventional Commits, as set in the global `CLAUDE.md` (`<type>[(scope)][!]: <summary>`).
- Summary: brief, lowercase except names and identifiers, starts with a verb, and says what changes in behavior. `fix(agent-runner): probe the owner while a call waits on it`.
- Add a body only when the reason is not clear from the summary and the diff: the symptom, the cause, or a rejected alternative. Do not list the changed files.
- No `Co-Authored-By` line.
