# Daemon — SWE-bench Lite artifacts (20260923_Daemon)

Artifacts for the SWE-bench Lite submission
[SWE-bench/experiments#493](https://github.com/SWE-bench/experiments/pull/493).
Agent source: https://github.com/Kapozux/Daemon

## Contents

| Path | What |
| --- | --- |
| `all_preds.jsonl` | The submitted predictions: one per instance, all 300 Lite instances. 23 have an empty `model_patch` (the agent produced no diff). |
| `logs/<instance_id>/` | `swebench.harness.run_evaluation` output for the 277 instances with a non-empty patch. |
| `trajs/<instance_id>.txt` | Task prompt given to the agent. |
| `trajs/<instance_id>.log` | Full agent trajectory (every model turn and tool/bash output) for the scored attempt. |
| `trajs/<instance_id>.diff` | `git diff` collected at the end of that attempt; identical to `model_patch` in `all_preds.jsonl`. |

## pass@1

Every file here belongs to the **first and only scored attempt** per instance.

The run harness supported re-rolling an instance whose diff came back empty, and the
original run did use one re-roll. Those second attempts are **not** part of the submission:
they are excluded from `all_preds.jsonl`, from the evaluation, and from `trajs/`.
Without them the score is 173/300 (57.67%).

An earlier version of this repo mistakenly put the second-attempt trajectory in `trajs/`
for the 23 empty-patch instances (the predictions and score were already first-attempt only).
They have been replaced with the first-attempt trajectories.
For `sympy__sympy-11400` the first-attempt stdout log was overwritten locally by a later,
unrelated run, so `trajs/sympy__sympy-11400.log` is the agent's own chat-history export
of that same first attempt (2026-09-21 10:42 UTC) — different format, same attempt.
