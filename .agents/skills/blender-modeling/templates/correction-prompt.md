Use the `blender-modeling` skill in multi-agent **correction** mode. Act as Coordinator.

Read `references/multi-agent-workflow.md`, `references/retry-policy.md`, and `workflow.yaml`. Initialize a task-scoped copy of `templates/iteration-state.yaml` with `mode: correction`. Load role prompts only as needed.

## Human feedback and evidence

- Feedback: `[observable concern, such as too thick or a detached-looking connection]`
- Reference: `[path]`
- Current front / side / three-quarter renders: `[paths]`
- Accepted Blender checkpoint: `[path]`
- Target region: `[region]`
- Protected regions and out-of-scope aspects: `[explicit scope]`

## Required behavior

- Start with read-only analysis. Planner makes a bounded plan; Coordinator approves before Blender changes.
- Derive approximate relative guidance from references without asking for invented exact dimensions.
- Only Modeler changes Blender; save a separate before checkpoint for each attempt.
- Correct one primary issue and at most one inseparable minor issue. Review independently for appearance and geometry.
- Reject neutral or regressed visual corrections. Preserve unresolved global gaps when returning to a creation stage.
- Count failed reviewed candidates separately from execution/protection incidents under the retry policy. Never reset the same defect by renaming it. Stop the affected branch at the applicable limit and report evidence.
- Apply any explicit user override to counters and stop scope before these defaults.
