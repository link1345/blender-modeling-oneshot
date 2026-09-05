# Multi-Agent Blender Correction Workflow

Use this workflow when a reference-driven correction has caused regressions, invented geometry, or repeated visual failure. It is intended for local corrections to an existing asset, not for making several agents independently remodel the whole object.

For a new asset, start with `creation-workflow.md` and enter this loop only for an identified defect. Use `retry-policy.md` for failure classification and stopping. Explicit user instructions override these defaults.

## Roles

The root agent acts as Coordinator. It does not need a separate sub-agent.

| Role | Reads Blender | Changes Blender | Output |
| --- | --- | --- | --- |
| Coordinator | As needed | No | state, routing, accept/retry/rollback decision |
| Visual Analyst | images only | No | observed visual differences and approximate relative corrections |
| Planner | scene metadata as needed | No | one bounded implementation plan |
| Blender Modeler | Yes | Yes | checkpoint, script, edited scene, renders |
| Visual Reviewer | images only | No | IMPROVED/NEUTRAL/REGRESSED and PASS/FAIL |
| Geometry Inspector | Yes, read-only | No | mesh and scene validation |

These are workflow permissions. If the runtime cannot technically enforce read-only Blender access, the Coordinator must enforce it through the role prompts and reject unauthorized edits.

## Required files

- Shared state: `templates/iteration-state.yaml`
- Declarative workflow contract: `workflow.yaml`
- Correction prompt: `templates/correction-prompt.md`
- Role prompts: `agent-prompts/*.md`
- Final geometry checklist: `references/quality-checklist.md`

Resolve all relative paths from the `blender-modeling` skill directory.

## Operating rules

1. The human may provide subjective feedback such as "too thick", "blob-like", or "looks attached from the side". Do not ask the human to invent exact dimensions when the references can support a relative estimate.
2. Use a stable visible feature as reference scale `1.0`. Record ranges or directional changes, not false precision.
3. Change one major issue per iteration. A second minor correction is allowed only when it is inseparable from the first.
4. Protect all regions outside the approved target.
5. Save a checkpoint before the Blender Modeler changes the scene.
6. The Blender Modeler must produce consistent before/after views.
7. The Visual Reviewer and Geometry Inspector evaluate independently. They may run in parallel after renders and the edited checkpoint exist.
8. Only the Coordinator accepts, retries, or rolls back a result.
9. A Modeler self-assessment is evidence, never the completion decision.
10. Never hide a failed shape under a new primitive or leave the obsolete shape inside the final result.
11. Carry whole-asset gaps forward. A local acceptance does not mark the originating creation stage or required delivery complete.

## Execution sequence

### 1. Initialize

The Coordinator initializes a task-scoped copy of `templates/iteration-state.yaml` (do not edit the source template during a modeling run), sets `mode: correction`, fills paths and feedback, records the current accepted checkpoint, and identifies a stable problem criterion and protected regions. Preserve the originating stage and outstanding global gaps when entering from creation mode.

### 2. Analyze

Spawn a Visual Analyst with `agent-prompts/visual-analyst.md`. Give it only the reference images, consistent current renders, human feedback, target region, and protected regions.

The Coordinator rejects analysis that:

- treats lighting or color as geometry when they are out of scope
- asserts hidden depth without evidence
- invents decorative structure
- lists more than three high-impact differences
- presents image estimates as exact measurements

### 3. Plan

Spawn a Planner with `agent-prompts/planner.md`. Supply the accepted state and Visual Analyst result. The plan must name the exact target objects or state how the Modeler will discover them without editing.

The Coordinator approves the plan only if it has:

- one primary objective
- explicit allowed and protected regions
- a specific modeling technique
- observable success criteria
- rollback conditions
- required output paths

### 4. Implement

Spawn one Blender Modeler with `agent-prompts/blender-modeler.md`. It is the only sub-agent authorized to edit the scene.

The Modeler must:

- inspect tools, Blender version, scene, objects, and scale first
- save a before checkpoint
- preserve or safely back up the current accepted geometry
- make only the approved bounded change
- save the reusable script under `blender/scripts/`
- save a candidate checkpoint under `blender/checkpoints/`
- render front, side, three-quarter, and target close-up views under `blender/renders/`
- report exact modified, created, hidden, and deleted objects

Use task-scoped paths so one attempt cannot overwrite another task's evidence:

- `blender/checkpoints/<task_id>/iteration_XX_before.blend`
- `blender/checkpoints/<task_id>/iteration_XX_candidate.blend`
- `blender/scripts/<task_id>/iteration_XX_<change>.py`
- `blender/renders/<task_id>/iteration_XX_front.png`
- `blender/renders/<task_id>/iteration_XX_side.png`
- `blender/renders/<task_id>/iteration_XX_perspective.png`
- `blender/renders/<task_id>/iteration_XX_closeup.png`

### 5. Review in parallel

After implementation finishes, spawn:

- Visual Reviewer using `agent-prompts/visual-reviewer.md`
- Geometry Inspector using `agent-prompts/geometry-inspector.md`

They must inspect the same candidate iteration. Neither may modify files or Blender state.

### 6. Decide

The Coordinator combines both reviews:

| Visual result | Geometry result | Decision |
| --- | --- | --- |
| IMPROVED + visual PASS | PASS | ACCEPT |
| IMPROVED + visual FAIL | PASS or warnings | RETRY one remaining visual issue |
| IMPROVED | blocking geometry failure | RETRY technical repair or ROLLBACK |
| NEUTRAL | any | ROLLBACK for a visual correction; use the technical-stage gate only if that scope was approved before execution and the user permits it |
| REGRESSED | any | ROLLBACK |
| any | protected region changed | ROLLBACK |

`PASS_WITH_LIMITATIONS` is allowed only when limitations do not violate the task's completion criteria and are recorded explicitly. Return an accepted local fix to its originating stage for whole-asset review. Missing required deliverables or defining reference features cannot be hidden in this status.

## Retry and stopping rules

- Apply `retry-policy.md`: reviewed candidate failures and execution/protection incidents have separate bounded counters. A render or context error before reliable review is not evidence of a repeated visual defect.
- Do not reset a defect's allowance by changing its suspected cause or renaming it. After two candidate failures, diagnose before another attempt; after three, stop that branch.
- Do not silently expand the target region.
- Do not exceed the runtime's available agent slots. Analysis, planning, and modeling are sequential; only the two independent reviews normally benefit from parallel execution.

## Final gate

Before completion:

1. Read and apply `references/quality-checklist.md` for all applicable sections.
2. Confirm the final accepted `.blend` is not merely the last attempted candidate.
3. Confirm validation renders correspond to that exact accepted file.
4. Record `PASS`, `PASS_WITH_LIMITATIONS`, or `FAIL` with reasons.
5. Report checkpoints, scripts, renders, geometry statistics, protected-region verification, and known limitations.
6. Label a local pass as local. Completion of the user's task additionally requires the whole-asset gate and required-delivery evidence described in `creation-workflow.md`.

## Runtime note

`workflow.yaml` is a declarative orchestration contract, not an executable agent runtime. In Codex, the root agent reads it and uses the available sub-agent delegation tools. Tool permissions such as `read_only` express required behavior; they are not a technical sandbox unless the host runtime enforces them.
