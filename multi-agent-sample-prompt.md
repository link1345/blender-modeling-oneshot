# Blender Multi-Agent Correction Prompt

The reusable start prompt is located at:

`.agents/skills/blender-modeling/templates/start-prompt.md`

Copy it into a new Codex task, replace the bracketed paths and descriptions, and attach the reference and current-render images. The root agent serves as Coordinator; it should spawn the specialist roles sequentially, with Visual Reviewer and Geometry Inspector running in parallel only after a candidate has been created.

For the antique clock-key example, the human feedback can be as simple as:

```text
The connector below the clock is too swollen and blob-like. The shaft is better than before, so preserve its length and the clock face, outer frame, top ring, and key bit. Ignore color and texture. Estimate relative corrections from the reference; do not ask me for exact dimensions.
```

This workflow does not provide hard technical sandboxing between agents. Its read-only and read-write boundaries are explicit operating rules enforced by the Coordinator. Only the Blender Modeler is authorized to alter the scene.

Candidate files are namespaced by task and iteration. For example:

```text
blender/checkpoints/clock-key-fix/iteration_01_before.blend
blender/checkpoints/clock-key-fix/iteration_01_candidate.blend
blender/scripts/clock-key-fix/iteration_01_connector_profile.py
blender/renders/clock-key-fix/iteration_01_front.png
```
