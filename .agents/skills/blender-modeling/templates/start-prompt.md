Use the `blender-modeling` skill in multi-agent **creation** mode. Act as Coordinator.

Read `references/creation-workflow.md`, `workflow.yaml`, and `templates/iteration-state.yaml`. Load role prompts only when needed. Initialize a task-scoped state copy; do not edit the template during production.

## Asset and references

- Asset and intended use: `[description]`
- Reference images and known views: `[paths and labels]`
- Existing scene to protect: `[path, or inspect the current scene]`
- Required appearance, scale, and technical constraints: `[requirements]`

Reference sheets are design evidence, not renders of a current model. Identify uncertain views and state inferred geometry before implementation.

## Delivery contract

- Required outputs and behavior: `[formats, static design, materials, rig/runtime needs, verification]`
- Explicitly optional features: `[features, or none]`

Do not downgrade required quality or behavior. Check uncertain dependencies early, secure and verify required delivery before optional experiments, and preserve that checkpoint.

## Workflow

- Begin with read-only Visual Analyst analysis, then a Planner stage plan approved by Coordinator.
- Only Blender Modeler edits Blender. Preserve existing data and save a separate checkpoint before changes.
- Review primary shape, reference appearance, and required delivery at coherent stage boundaries. Do not run the full delegation cycle for each small operation.
- Visual Reviewer and Geometry Inspector independently review each stage. Evaluate the whole reference match, and carry unresolved global gaps forward.
- Use `references/multi-agent-workflow.md` only for identified local defects, then return to the stage gate.
- Use `references/retry-policy.md`: count reviewed candidate failures separately from execution incidents; both are bounded. Stop the affected branch at its limit. Optional failure must not discard required delivery.
- Respect any stricter stopping or neutral-result rule I explicitly provide. A first blockout is assessed against references, and a technical stage must show actual technical evidence rather than invented visual improvement.

Do not declare completion until every required deliverable is verified and the whole-asset review has no blocking gaps. Report target-runtime limitations separately from Blender preview results.
