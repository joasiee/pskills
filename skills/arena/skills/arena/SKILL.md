---
name: arena
description: "Spawn N parallel candidates at the same task, pick a base, graft the strongest parts of the losers into it. Use for /arena, 'arena this', 'throw it in the arena', or when one attempt at a non-trivial artifact would lock in the wrong shape."
disable-model-invocation: true
---

# Arena

Open a todo list with one entry per phase (Frame, Fan out, Cross-judge, Pick, Graft, Verify) before launching anything.

## Phase A: Frame

Every candidate gets the same prompt, so the prompt is the contract.

1. State the artifact each candidate is producing. When building or running a candidate is expensive, such as a large native build per worktree, ask for a design artifact instead of a full implementation: signatures with stub bodies, a short design note, or the algorithm in isolation.
2. Derive the rubric, 3-6 concrete gradeable criteria for what success looks like on *this* task. It is the picker's tool in Phase D. Candidates only see the task.
3. Pick the runners. Use the models and count the user names. Otherwise run 2 candidates on `model: "opus"` with `effort: "high"`, or `effort: "medium"` for a small question such as a name or where a type lives. Add a third candidate when the task has more than one design direction worth covering. Add a `model: "fable"` candidate when the user wants a second model's take.
4. Give each candidate its own output location, so no two candidates write the same files: `isolation: "worktree"` for code, otherwise a folder of its own in the scratchpad, such as `arena-<slug>/candidate-<n>/`.

## Phase B: Fan out

Spawn all N candidates in one message as `general-purpose` agents, each with the task, the paths to the shared grounding, its own output path, and instructions to produce the artifact and a short rationale naming the alternatives it considered and what it rejected.

If a candidate produces no output, proceed with N-1 and note the dropout.

## Phase C: Cross-judge

After all Phase B candidates complete, spawn one read-only judge (`Explore`, told not to edit files) on a model that no candidate ran on: `model: "sonnet"` with `effort: "xhigh"` by default. A model rates its own outputs higher than other models rate them, so the judge never shares a model with the candidates. If every model ran a candidate, skip the judge, pick the base alone in Phase D, and say so.

The judge sees the rubric and the candidates by path label, scores each criterion, and recommends a base with rationale. It runs in parallel with your reading in Phase D.

## Phase D: Pick a base

Read every candidate end to end before picking. Score each against the rubric criterion by criterion, not on holistic feel, and compare with the judge. You may share a model with the candidates, so the per-criterion scores are your guard against favoring one. Agreement on the base confirms the pick. Disagreement means one of you is biased or the rubric was ambiguous. Read both rationales before deciding.

Pick the base a future maintainer can extend most easily without breaking invariants. When two feel tied, prefer the cleaner boundary or smaller API.

## Phase E: Graft

Walk each losing candidate once more for what is worth porting into the base, usually one or two things per candidate, not most of it. Fold each graft in by hand, reshaping the base where needed, so the result reads as one design under one mental model. Don't paste mechanically.

If the candidates converge on one shape, note it and ship the consensus shape. No graft is needed. Candidates on the same model converge more easily than candidates on different models, so read convergence as support, not proof. If they wildly diverge, Phase A was under-specified. Reframe and re-run rather than averaging the divergence.

## Phase F: Verify

Verify the synthesized artifact against the real thing: build and run the code, or check the design against the code it must fit. A self-report or "it compiles" is not verification. If verification finds a problem the arena missed, either Phase A was wrong (re-frame and re-run) or a candidate caught it and you missed the graft (go back to Phase E). Don't paper over it.

## Outputs

One synthesized artifact, with a short synthesis note alongside naming the base and why, the judge's verdict or that Phase C skipped the judge, each graft with its source candidate, what was rejected and why, any convergence or dropouts, and the verification result.
