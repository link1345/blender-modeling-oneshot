# Blender MCP Project Instructions

## Purpose

This repository uses Blender through MCP and Blender Python to create, modify, inspect, and validate 3D assets.

For Blender modeling tasks, use the `blender-modeling` skill whenever it is available.

## General Blender rules

- Treat Blender MCP as an execution and observation interface, not merely as a primitive-placement interface.
- Prefer reproducible Blender Python scripts over long sequences of fragile UI operations.
- Store reusable Blender scripts under `blender/scripts/`.
- Store checkpoint files under `blender/checkpoints/`.
- Store validation renders under `blender/renders/`.
- Never overwrite the only usable `.blend` file.
- Save a checkpoint before destructive or difficult-to-reverse operations.
- Do not claim visual success without inspecting rendered or viewport images.
- Do not claim geometry quality without running mesh validation.

## Modeling policy

Primitive objects may be used as starting geometry, cutters, guides, or temporary construction objects.

Primitive objects must not be used as the final result when the requested object requires a continuous, shaped, or organic surface.

For complex modeling, use one or more of the following as appropriate:

- direct vertex, edge, and face manipulation
- Blender Python `bmesh`
- extrusion
- inset
- bevel
- loop cuts
- proportional editing
- subdivision surfaces
- mirror modifiers
- shrinkwrap modifiers
- solidify modifiers
- boolean modifiers
- lattice deformation
- curves
- sculpting or voxel remesh
- geometry nodes
- retopology

Do not choose a technique merely because it is easy to automate. Choose it because it matches the intended shape and downstream use.

## Execution policy

Before changing the scene:

1. Inspect the available MCP tools.
2. Inspect the current Blender version and scene.
3. Identify reference images, existing meshes, rigs, materials, and scale conventions.
4. Write a short modeling plan.
5. Define measurable completion criteria.

When arbitrary Blender Python execution is available, prefer it for deterministic mesh construction and validation.

When a Blender operator depends on selection, mode, area, or active-object context, explicitly establish that context before invoking it.

## Iteration policy

Complex assets must be created iteratively.

For new assets, plan coherent stages: primary shape, reference appearance, and required delivery. Complete and verify required deliverables before attempting optional features. A stage may contain several related modeling operations; do not run the full multi-agent correction cycle for every small operation. Use that cycle for an identified local defect.

At each stage boundary, compare the whole asset to the reference as well as the edited region. A sequence of local passes does not establish overall completion. Classify failed candidates separately from tool, environment, and protection-check incidents using the skill's retry policy; explicit user stopping rules take precedence.

For every major modeling stage:

1. Implement the approved stage, or one bounded defect correction when in correction mode.
2. Save or update the generating script.
3. Execute the change.
4. Inspect the result from multiple views.
5. Compare it against the reference and requirements.
6. Record the most important defects.
7. Fix the highest-impact defects first.
8. Save a checkpoint when the stage is acceptable.

Do not continue blindly after an unexpected result.

## Validation policy

Before declaring completion, verify at least:

- object count
- object names
- dimensions and scale
- transform application status
- polygon and vertex counts
- non-manifold geometry
- duplicate vertices
- loose geometry
- inverted or inconsistent normals
- internal faces where relevant
- visible intersections
- modifier stack
- symmetry where required
- subdivision behavior where required
- silhouette from required views
- deformation behavior for rigged assets
- material assignment where required

A task is not complete solely because the Blender command or Python script executed without errors.

## Reporting policy

At completion, report:

- what was created or changed
- which modeling techniques were used
- scripts that were created
- checkpoints that were saved
- validation that was performed
- known limitations
- paths of final `.blend`, scripts, and rendered inspections

If visual inspection or mesh validation could not be performed, state that clearly.
