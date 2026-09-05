# In-Scene Reference Comparison

Use for reference-driven shape creation or correction when a usable view is available. Prefer an aligned image behind the model in Blender so silhouette and landmark differences can be inspected directly. This supports, but does not replace, unobstructed solid and perspective inspection. Capture-only requests do not require a new reference setup.

## Plan before placing images

The read-only Visual Analyst identifies view labels, projection uncertainty, useful image regions, and landmarks. The Planner records the source image and crop, corresponding model view, alignment anchors, scale basis, and which reference takes priority if drawings disagree. Coordinator approves this setup as part of the stage plan; only Modeler changes Blender, including reference objects and cameras.

- Separate views on a reference sheet by display framing or non-destructive crops, retaining the original and crop coordinates. Preserve aspect ratio; do not stretch or warp a drawing to fit the model.
- For a credible front or side drawing, use the corresponding orthographic view. Align a centerline and separated landmarks such as top/bottom endpoints; use known dimensions when supplied, otherwise record relative scale as an assumption.
- A perspective or stylized illustration is not a precise orthographic blueprint. Use an approximate matched view or side-by-side comparison and report its limits. Do not flatten the model or distort a view to satisfy incompatible outlines; record conflicts and the chosen priority before modeling.

## Modeler setup and iteration

1. Save a separate before checkpoint. Prefer image reference empties in a dedicated reference collection, separate from asset geometry. Lock selection after alignment. Keep references out of beauty renders and asset exports; a textured plane fallback needs explicit render/export exclusion.
2. Set usable transparency and depth/display settings so the model silhouette or wireframe and reference are both readable. Record image/crop, object transforms, view/projection, framing, and anchors in `reference_alignment` in task state. Keep image dependencies available with the working `.blend`.
3. Capture an aligned overlay at blockout and relevant shape-review gates, together with a clean view and a perspective view. Inspect actual pixels; reference objects may not appear in a standard render. Use viewport capture or an isolated comparison setup when needed, without altering asset materials for the overlay.
4. Keep the same alignment and framing for before/candidate comparisons. Do not move or rescale the reference to hide a defect. If calibration itself was wrong, document why, obtain Coordinator approval, and recapture both states with the corrected alignment before judging improvement.
5. At delivery, verify reference helpers are absent from the exported asset and clean presentation images. Retain the setup in the working file when useful, with references hidden by default for presentation.

## Independent review

Visual Reviewer checks overlay registration, silhouette and landmarks, then the clean and perspective views for thickness, intersections, and material appearance that an overlay can obscure. An unreadable or mismatched overlay is insufficient evidence, not a model pass. Geometry Inspector checks reference/asset separation and export exclusion from actual evidence. If tools cannot provide an aligned capture, record the limitation and use consistently framed side-by-side images; do not claim an overlay was inspected.
