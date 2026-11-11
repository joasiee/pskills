# pskills

Personal Claude Code skills.

## Rule: no sensitive information

**This repository is public. Keep sensitive information out of it at all cost.** This
applies to skills, examples, the README, commit messages and commit metadata:

- No employer, customer, colleague or partner names.
- No internal product names, code names, class or function names, file paths, repos,
  branches, environments, hostnames or infrastructure details.
- No ticket, work item or PR numbers, and no real incidents, dates or figures from work.
- No credentials, tokens, links to internal systems, or personal data.
- Commit with the GitHub no-reply address as author email, never a work address.

Write examples with invented, generic names (`Acme`, `JobQueue`, `release/2.4`), or describe
the case without names. Read the full diff before every commit. When in doubt, leave it out.

## Available skills

| Skill            | Description                                                                                                                            |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `better-writing` | Writing style for text that leaves the session: PR and work item text, commit messages, proposals, chat messages, customer-facing text |
| `comment-pass`   | Sonnet scan of the comments and docs a branch adds, then fix and commit them as a docs commit where possible                           |
| `benchmark-checklist` | Vet a measured performance number before reporting it: limiter, tuning, errors, interleaved repeat runs, end-to-end share         |
| `blast-radius`   | What a small change breaks outside its diff, with the one fact it is safe because of proven by running code                           |
| `correct`        | Turn mistakes agents keep repeating into checks that fail: architecture, types, lints and hooks, tests, docs last                      |
| `arena`          | Independent candidates at the same task, a judge on another model, then pick a base and graft the best parts                          |
| `writing-for-agents` | Writing skills, AGENTS.md and CLAUDE.md, and subagent prompts: pointers, hierarchy, completion criteria, leading words, pruning |

## Third-party skills

`benchmark-checklist`, `blast-radius`, `correct` and `arena` come from [pstack](https://github.com/cursor/plugins/tree/main/pstack)
by Lauren Tan, MIT licensed, at commit `5866df5`. Each one's plugin folder holds the original `LICENSE`. The changes adapt
them to Claude Code: Claude models and the `Agent` tool instead of Cursor's `Task` and Grok, Windows commands next to Linux
ones, and no references to pstack skills that aren't copied here.

`writing-for-agents` comes from [mattpocock/skills](https://github.com/mattpocock/skills) by Matt Pocock, MIT licensed, at
commit `4ae2317`. Its plugin folder holds the original `LICENSE`. The change adds subagent prompts to the documents it
covers and to its trigger. The Codex `agents/openai.yaml` is left out.

## Setup

1. In Claude Code, register the marketplace directly from the git URL:

```
/plugin marketplace add https://github.com/joasiee/pskills.git
```

2. Install individual skills:

```
/plugin install better-writing@pskills
```

## Adding a new skill

Each entry in `marketplace.json` is a Claude Code **plugin**, and a plugin exposes its
skill(s) via its own internal `skills/<skill-name>/SKILL.md`. That is a Claude Code
plugin requirement, separate from this repo's own top-level `skills/` folder (which just
groups plugin sources side by side). The two nest, so the real path ends up:

```
skills/<skill-name>/skills/<skill-name>/SKILL.md
```

1. Create that nested folder: `skills/<skill-name>/skills/<skill-name>/`
2. Add `SKILL.md` there, with the skill frontmatter and instructions, following the
   [no sensitive information rule](#rule-no-sensitive-information)
3. Register the _outer_ folder as the plugin's source in `.claude-plugin/marketplace.json`:
   `"source": "./skills/<skill-name>"`
4. Commit and push
