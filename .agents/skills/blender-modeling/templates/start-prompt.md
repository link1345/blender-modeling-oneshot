Use the `blender-modeling` skill and its multi-agent correction workflow for this task.

Act as the Coordinator. Read `references/multi-agent-workflow.md`, then load role prompts from `agent-prompts/` only when that role is needed. Initialize shared state from `templates/iteration-state.yaml`.

## Human feedback

[Write subjective feedback here. Examples: too thick, blob-like, angular, looks pasted on, or less delicate than the reference.]

## References

- Reference image: `[path]`
- Current front render: `[path]`
- Current side render: `[path]`
- Current three-quarter render: `[path]`
- Current accepted Blender file: `[path]`

## Scope

- Target region: `[region]`
- Protected regions: `[regions that must not change]`
- Out of scope: color, materials, textures, and lighting unless explicitly stated otherwise

## Required behavior

- Do not ask me to invent exact dimensions. Derive approximate relative guidance from the supplied images and state uncertainty.
- Correct one major issue per iteration.
- Only the Blender Modeler may change the scene.
- Save a checkpoint before every attempted change.
- Review the candidate visually and geometrically before accepting it.
- Roll back neutral or regressed candidates.
- Stop after three failed attempts on the same problem and report the likely cause.

Begin with read-only analysis. Do not modify Blender until the Visual Analyst result has been converted into an approved bounded plan.
