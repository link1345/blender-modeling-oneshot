---
name: blender-modeling
description: Create, modify, repair, or validate non-trivial Blender 3D models through Blender MCP or Blender Python. Use for mesh modeling, sculpting, retopology, modifiers, reference-image matching, UV-aware asset work, rig-ready geometry, and iterative visual inspection. Do not use for simple scene questions or tasks that only require placing unchanged primitives.
---

# Blender Modeling Skill

## Objective

Produce intentionally shaped, inspectable, and reproducible Blender assets.

The goal is not merely to make a scene that vaguely resembles the request. The goal is to create appropriate geometry using a modeling process that can be inspected, repeated, and improved.

Before final validation, read `references/quality-checklist.md` and complete all applicable sections. Do not load or execute every section mechanically during early blockout work.

When multi-agent work is requested, select its mode before editing:

- **New asset:** read `references/creation-workflow.md`. Review coherent stages, then use the local correction loop only for identified defects.
- **Existing asset correction:** read `references/multi-agent-workflow.md`. Keep each correction to one primary issue.
- **Capture only:** use the capture guidance in `references/creation-workflow.md`; do not restart modeling to provide images.

For these modes, `workflow.yaml` defines routing and `references/retry-policy.md` defines failure accounting. Load only role prompts needed for the current phase. Also use the correction workflow when reference matching has produced regressions, contradictory fixes, or invented geometry.

## Core principle

Do not confuse object assembly with modeling.

A group of cubes, spheres, cylinders, or capsules is not an acceptable final model when the target requires:

- a coherent silhouette
- continuous surfaces
- anatomical or organic form
- fitted clothing
- manufactured surface transitions
- controlled topology
- deformation
- subdivision
- UV mapping
- close reference-image matching

Primitives may be used for blockout, boolean cutters, guides, or base meshes. They must then be transformed into suitable final geometry.

## Phase 0: Discover available capabilities

Before modeling, inspect the Blender MCP tools and determine whether the environment supports:

- arbitrary Blender Python execution
- scene inspection
- object listing
- mesh statistics
- viewport screenshots
- rendered images
- camera or viewport orientation
- file save and load
- modifier creation
- Edit Mode operations
- selection of vertices, edges, and faces
- sculpt operations
- access to console errors

Do not assume a tool exists.

If arbitrary Blender Python execution exists, use it as the primary mechanism for deterministic operations.

If only high-level primitive tools exist, state that the available MCP interface is insufficient for the requested modeling quality instead of pretending that primitive assembly is a finished result.

## Phase 1: Inspect the task and source material

Inspect:

- all reference images
- requested viewing angles
- intended use of the asset
- expected scale
- required topology quality
- whether it will be rigged or animated
- whether subdivision is expected
- whether the model must fit an existing body or mesh
- polygon budget
- texture and UV requirements
- symmetry or asymmetry
- required file format

When reference images are available, identify:

- primary silhouette
- large proportions
- landmarks
- cross-sectional changes
- hard and soft transitions
- overlapping parts
- symmetry
- ambiguous or hidden regions

Separate observed facts from inferred geometry.

## Phase 2: Define success before editing

Write a concise task-specific completion checklist.

At minimum include:

- target dimensions or relative proportions
- required views
- silhouette requirements
- topology requirements
- allowed polygon range
- required modifiers
- forbidden shortcuts
- output file path
- required validation images

Do not start detailed modeling until this checklist exists.

Separate required deliverables from explicitly optional features. Preserve the user's requested quality and functionality in the required list; do not downgrade them to make a baseline easier. Check uncertain tool/export capabilities early. Secure a verified required-delivery checkpoint before optional experiments, and keep it available if an experiment fails.

## Phase 3: Choose the modeling strategy

Select a strategy based on the object.

### Hard-surface objects

Prefer combinations of:

- profile construction
- extrusion
- inset
- bevel
- loop cuts
- booleans followed by cleanup
- mirror
- weighted normals
- subdivision where appropriate

Do not approximate designed transitions by intersecting untouched primitives.

### Organic objects

Prefer combinations of:

- low-resolution base mesh
- mirror
- proportional editing
- subdivision
- sculpting
- voxel remesh where appropriate
- shrinkwrap
- retopology

Do not preserve primitive silhouettes such as obvious spheres or capsules unless the reference genuinely contains them.

### Clothing

Prefer:

- modifying an existing garment or body-compatible base mesh
- mirror
- shrinkwrap with controlled offset
- solidify
- proportional editing
- sculpting for folds
- retopology for deformation
- fitting tests against the target body

Do not create fitted clothing solely by placing flattened cubes or intersecting cylinders around the body.

### Repeated or procedural structures

Prefer Geometry Nodes or generated mesh scripts when repetition, parameterization, or reproducibility is central.

## Phase 4: Create a blockout

Create only the large forms first.

The blockout must establish:

- overall dimensions
- major silhouette
- major mass distribution
- orientation
- symmetry
- part relationships

Use the lowest complexity that can represent the silhouette.

Do not add small details before the large proportions have been inspected.

After blockout:

1. capture front view
2. capture side view
3. capture rear view if relevant
4. capture perspective or three-quarter view
5. compare against references
6. list the three largest discrepancies
7. fix those discrepancies before proceeding

An absent starting model is not a failed comparison: assess the first blockout against reference criteria and record the before comparison as `NOT_APPLICABLE`. Do not call a new shape improved merely because an empty scene now contains objects.

## Phase 5: Convert blockout into modeled geometry

After the blockout is accepted, replace temporary construction with appropriate geometry.

Use Blender Python and `bmesh` where direct mesh editing is needed.

Prefer explicit, deterministic operations such as:

- creating vertices and faces from measured coordinates
- extruding selected regions
- subdividing selected edges
- beveling selected edges
- dissolving unnecessary geometry
- merging close vertices
- recalculating normals
- selecting geometry by position or topology rather than fragile screen coordinates

Avoid long chains of UI actions that depend on an uncertain viewport state.

Keep generated scripts idempotent when practical.

An idempotent script should either:

- recreate its own collection or named objects safely, or
- detect existing generated objects and update them deliberately.

## Phase 6: Iterative visual correction

After every major stage, inspect multiple views.

Use the following correction loop:

1. Render or capture consistent views.
2. Compare silhouette and landmarks.
3. Identify the largest visible error.
4. Form a concrete geometric hypothesis.
5. Make one bounded correction.
6. Capture the same views again.
7. Determine whether the correction improved the result.
8. Keep, revise, or revert it.

Do not make many unrelated changes between inspections.

For the multi-agent workflow, the coordinating agent must keep authorship and review separate. Only the Blender Modeler may change the scene. The Visual Analyst, Planner, Visual Reviewer, and Geometry Inspector return findings or plans without editing Blender files.

For new assets, the loop runs at meaningful stage boundaries rather than after every small operation. Review the whole reference match at those boundaries, including materials and defining details when in scope. Keep unresolved global gaps in shared state until fixed or explicitly removed from scope by the user. A local `PASS` must not erase them.

When comparing against a reference, prioritize in this order:

1. overall silhouette
2. proportions
3. placement of major landmarks
4. cross-sectional shape
5. transitions between forms
6. secondary forms
7. surface detail

## Phase 7: Topology and technical cleanup

Run cleanup appropriate to the asset.

Check:

- duplicate vertices
- loose vertices and edges
- non-manifold edges
- internal faces
- zero-area faces
- degenerate geometry
- overlapping coplanar faces
- inconsistent normals
- extreme thin triangles
- unintended poles
- unsupported long n-gons
- visible boolean debris
- unapplied scale affecting modifiers
- accidental disconnected islands

Use triangulation only when required by the target pipeline. Do not triangulate merely to hide poor topology.

For subdivision-ready assets:

- inspect the unsubdivided cage
- inspect the subdivided result
- verify that edge support is intentional
- verify that the silhouette does not collapse
- avoid uncontrolled pinching

For rigged or deforming assets:

- inspect edge flow around bending regions
- run simple deformation tests
- check for volume loss and intersections

## Phase 8: Save and validate

Save staged checkpoints using meaningful names, for example:

- `checkpoints/01_blockout.blend`
- `checkpoints/02_primary_forms.blend`
- `checkpoints/03_topology.blend`
- `checkpoints/04_final.blend`

Do not overwrite all stages with a single file.

Create validation captures with stable names:

- `renders/front.png`
- `renders/side.png`
- `renders/back.png`
- `renders/perspective.png`
- `renders/wireframe.png`

Before completion, report:

- dimensions
- vertex count
- edge count
- face count
- object count
- modifier list
- non-manifold count
- loose geometry count
- whether normals were checked
- whether duplicate vertices were checked
- whether front, side, and perspective views were inspected

## Failure handling

If an operation fails:

1. stop the current modeling branch
2. inspect the Blender error
3. inspect active object, mode, and selection
4. restore the most recent valid checkpoint if necessary
5. revise the script or operation
6. rerun only the failed stage

Use `references/retry-policy.md` to distinguish a reviewed candidate failure from an execution or protection incident. A rollback is required for protected-data damage regardless of which counter changes. Never rename the same unresolved defect to reset its allowance.

Do not respond to failure by adding unrelated primitives.

If the visual result is poor:

- do not describe it as complete
- identify why the silhouette or topology is wrong
- return to the earliest incorrect stage
- correct major forms before adding detail

## Completion gate

Do not declare completion until all applicable conditions are satisfied:

- The requested object is recognizable from silhouette alone.
- The final geometry is not merely an assembly of unchanged primitives.
- The major proportions have been inspected from at least two orthographic views.
- A perspective view has been inspected.
- Mesh validation has been performed.
- The model is suitable for its stated downstream use.
- Final files and validation images have been saved.
- Known shortcomings have been stated honestly.
- Every required deliverable has recorded verification evidence, and the whole-asset reference review has no unresolved blocking gaps. Optional experiments cannot invalidate the accepted required-delivery checkpoint.

## Final response format

Provide:

1. Summary
2. Modeling approach
3. Major corrections made during iteration
4. Validation results
5. Output files
6. Known limitations
