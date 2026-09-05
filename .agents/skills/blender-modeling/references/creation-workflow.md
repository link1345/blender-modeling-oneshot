# Multi-Agent Creation and Capture Workflow

Use this mode for a new asset or a substantial build, rather than applying a local correction workflow to every part. The Coordinator stays in the root agent. Only the Blender Modeler edits Blender; the Analyst, Planner, Visual Reviewer, and Geometry Inspector remain read-only. Shared role permissions and paths are in `workflow.yaml`.

## Establish the delivery contract

Start with read-only reference analysis. If there is no current model, analyze intended proportions, landmarks, material character, and uncertainty without inventing a before-model comparison. The Planner then proposes coherent stages and the Coordinator approves them before Blender changes.

Record in a task-scoped copy of `templates/iteration-state.yaml`:

- Required deliverables, their verification method, and dependencies. Include requested export formats, rigging, static design elements, materials, and runtime behavior as applicable.
- Features the user explicitly made optional. Difficulty alone does not make a requirement optional.
- Whole-asset reference criteria: silhouette, proportions, defining details, and material character. Identify which are needed at each stage and which block final delivery.
- Assumptions, protected source data, allowed inspection-state changes, and what the relevant bounds measure: a base mesh, attached detail, or complete assembly.

Plan cheap capability checks for uncertain shaders, rigs, and export paths early. Use isolated minimal probes when useful; they are not finished deliverables. For example, a requested clock can have its static hands and required export verified before an optional ticking experiment. Do not postpone mandatory rigging or file delivery behind that experiment.

## Review at stage boundaries

For reference-driven shape stages, include the in-scene comparison setup from `reference-alignment.md` in the approved plan. Reuse its alignment through blockout and corrections rather than setting up a new comparison for every operation.

Typical stages are **primary shape**, **reference appearance**, and **required delivery**. Adapt their order and subdivisions to dependencies; this is not a fixed number of tool calls.

For each stage:

1. Planner specifies one coherent objective, related operations, scope, success criteria, and required evidence. Related pieces of a new assembly may be built together.
2. Coordinator approves the stage. Modeler inspects the live scene, saves a separate before checkpoint, and implements it. Modeler inspects intermediate results and saves checkpoints before destructive or difficult-to-reverse operations. Routine operations do not require a new round of delegation.
3. Modeler supplies a candidate, stable views of the whole asset and relevant close-ups, source-preservation evidence, and technical validation.
4. Visual Reviewer and Geometry Inspector independently review the same candidate. Run these two reviews in parallel where possible. The Coordinator alone decides acceptance.
5. If a specific defect blocks the stage, use `multi-agent-workflow.md` for that defect, then return to the stage gate. Keep unrelated accepted work protected.

At every gate, distinguish **stage acceptance** from **whole-asset readiness**. Early stages may defer detail to a named later stage; record the gap instead of repeatedly treating it as out of scope. Before accepting appearance, compare overall character to the reference, not only whether ornaments exist or materials have the expected names. No new unsupported detail should be invented to increase visual complexity.

For visual changes, require reference progress with no blocking regression. For the first blockout, use reference-based criteria with `NOT_APPLICABLE` before comparison. For a required technical stage whose appearance should stay unchanged (such as export), `NEUTRAL` is acceptable only with explicit technical verification and no visual regression. An explicit user rule rejecting all neutral candidates overrides this default; do not manufacture an improvement claim.

## Secure required delivery before optional work

Verify the requested deliverables, not just the script exit status. Check the final file exists and inspect a re-import when applicable; separately record what was tested in Blender and what was tested in the target runtime. Configuration instructions alone do not prove required runtime behavior.

Retain `required_delivery_checkpoint` and the verified required output paths. Optional work begins from a separate checkpoint only after all required deliverables are verified, unless the user explicitly chooses another order. An optional failure rolls back that branch without replacing the usable baseline. Follow `retry-policy.md` for counters and stop scope; a user instruction to stop all work still wins.

Final completion requires the whole-asset review, all required verification evidence, and no unresolved blocking gaps. A missing requirement cannot be relabeled as a limitation. Report optional omissions and nonblocking simplifications separately.

## Capture-only requests

For images of an accepted asset, use a brief capture plan and approved source checkpoint. Change only inspection cameras/display or isolated copies; preserve the asset and restore its state afterward. Save a before checkpoint if scene changes are necessary. Only the Modeler operates Blender.

Check requested angles, full framing, display-mode readability, and source preservation. Review the images independently and use a proportionate read-only preservation check; do not repeat full modeling validation or demand `IMPROVED` geometry. Record ambiguous display terminology as an assumption, or ask only if it materially changes what must be delivered.
