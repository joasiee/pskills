# PR description

When another skill or a template owns the structure, such as `## Summary` and `Fixes #<ID>`, keep it. This file sets what goes inside. Markdown renders.

Leave out the `## Test plan` section in every PR, also when a template has one. Nobody uses it, and it makes the PR noisier to read.

The reader is a reviewer who knows the codebase but not this change. They read the summary, then the diff.

## Summary

- Open with the problem or goal in one to three sentences, even when the work item has the full story. For a bug: the symptom, how to hit it, and the cause.
- Then the changes as bullets. One bullet per change the reviewer must understand, one or two sentences each, no bold leads.
- Say what changed and why. The diff shows how. Add a detail only when the reviewer cannot see it in the diff or would misread it: a non-obvious reason, an invariant, a behavior change, a rejected alternative.
- A small fix needs no bullets. More than about six bullets means the PR does several things. Group them, or say so.
- End with what the reviewer must know before merging, if anything: a deploy order, a config dependency, a known and accepted gap.
- Link, do not repeat: `PR !123`, `#456`.

## Example

A PR description the user approved as written apart from its test plan:

```markdown
## Summary

- The CSV export wrote one report per source file under `<output dir>/exports/<job id>/`, mirroring the folder tree of the source data. On deep network shares the report path plus the writer's `.tmp` suffix exceeded `MAX_PATH`, so every report failed to open (`path too long`) and the downloaded zip was empty.
- Reports are now staged in a short folder under the system temp dir, `export_<unique id>`, and `on_finish` zips that folder to the same path as before (`<job id>.zip`). The staging folder is removed after zipping, or when zipping fails.
- `make_temp_dir()` is not used because it is thread-local and removed on thread exit, while worker jobs write the reports and `on_finish` zips them.

Fixes #123
```
