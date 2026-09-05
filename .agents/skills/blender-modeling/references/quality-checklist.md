# Blender Modeling Quality Checklist

Use this checklist before declaring a Blender modeling task complete.

Not every item applies to every asset. Mark non-applicable items explicitly instead of silently skipping them.

---

## 1. Task and reference compliance

- [ ] The intended use of the model is documented.
- [ ] The expected scale and units are documented.
- [ ] Required reference images were inspected.
- [ ] Missing or ambiguous reference information was identified.
- [ ] Any inferred geometry was documented.
- [ ] The final result satisfies the task-specific completion criteria.
- [ ] The model was not declared complete merely because a script executed successfully.
- [ ] Required deliverables and user-optional features are listed separately.
- [ ] Whole-asset reference gaps survived local reviews and all blocking gaps are resolved before delivery.
- [ ] Optional work did not replace or damage the verified required-delivery checkpoint.

---

## 2. Overall shape and silhouette

Inspect the model from consistent orthographic and perspective views.

### Required views

- [ ] Front view inspected.
- [ ] Side view inspected.
- [ ] Rear view inspected when relevant.
- [ ] Top or bottom view inspected when relevant.
- [ ] Three-quarter perspective view inspected.
- [ ] Wireframe view inspected.

### Silhouette

- [ ] The model is recognizable from silhouette alone.
- [ ] The overall width, height, and depth are appropriate.
- [ ] Major proportions match the reference or specification.
- [ ] Primary masses are positioned correctly.
- [ ] Major landmarks are correctly placed.
- [ ] Cross-sectional changes are intentional.
- [ ] No primitive-like silhouette remains unintentionally.
- [ ] No visible gaps exist between surfaces that should be continuous.
- [ ] No obvious intersections exist between parts that should not intersect.
- [ ] No unexpected bumps, dents, or flat areas are visible.

### Reference comparison

- [ ] Front silhouette compared against the reference.
- [ ] Side silhouette compared against the reference.
- [ ] Perspective proportions compared against the reference.
- [ ] The three largest visible discrepancies were identified.
- [ ] High-impact discrepancies were corrected before secondary detail was added.
- [ ] Defining details and material character were compared across the whole asset; local passes were not substituted for overall fidelity.

---

## 3. Object and scene organization

- [ ] Objects have meaningful names.
- [ ] Collections have meaningful names.
- [ ] Temporary construction objects were removed or clearly labeled.
- [ ] Boolean cutters are hidden, organized, or removed as appropriate.
- [ ] Unused objects were removed.
- [ ] Duplicate objects were removed.
- [ ] No unexpected hidden objects remain.
- [ ] The final asset is located near the intended world origin.
- [ ] Object origins are placed intentionally.
- [ ] Parent-child relationships are correct.
- [ ] Collection hierarchy is suitable for export and maintenance.

---

## 4. Dimensions and transforms

- [ ] Scene units are correct.
- [ ] Model dimensions were measured.
- [ ] Scale matches the target pipeline.
- [ ] Object scale was checked.
- [ ] Rotation was checked.
- [ ] Location was checked.
- [ ] Transforms were applied where required.
- [ ] Unapplied transforms are intentional and documented.
- [ ] Modifier behavior is not distorted by unapplied scale.
- [ ] Negative scale is not causing inverted normals or export problems.

Record:

```text
Dimensions:
Location:
Rotation:
Scale:
Unit system:
```

---

## 5. Mesh integrity

Run programmatic or Blender-native validation where possible.

### Geometry validity

- [ ] Duplicate vertices checked.
- [ ] Merge-by-distance result reviewed.
- [ ] Loose vertices checked.
- [ ] Loose edges checked.
- [ ] Loose faces checked.
- [ ] Non-manifold edges checked.
- [ ] Boundary edges reviewed.
- [ ] Zero-area faces checked.
- [ ] Zero-length edges checked.
- [ ] Degenerate geometry checked.
- [ ] Internal faces checked.
- [ ] Overlapping coplanar faces checked.
- [ ] Self-intersections checked when relevant.
- [ ] Accidental disconnected mesh islands checked.
- [ ] Hidden geometry checked.
- [ ] Boolean debris checked.

Record:

```text
Duplicate vertex count:
Loose vertex count:
Loose edge count:
Loose face count:
Non-manifold edge count:
Disconnected island count:
```

---

## 6. Normals and shading

- [ ] Face orientation overlay inspected.
- [ ] Normals face outward where expected.
- [ ] Inconsistent normals were recalculated or corrected.
- [ ] Custom split normals were checked.
- [ ] Auto Smooth or equivalent shading setup was checked.
- [ ] Sharp edges are intentional.
- [ ] Smooth-shaded surfaces appear smooth.
- [ ] Hard-surface edges retain intended definition.
- [ ] No unexplained dark patches appear.
- [ ] No visible shading seams appear unexpectedly.
- [ ] Weighted Normal modifier behavior was checked when used.

---

## 7. Topology quality

### General topology

- [ ] Edge flow follows the form.
- [ ] Edge density is appropriate for the shape.
- [ ] Polygon density is not unnecessarily high.
- [ ] Polygon density is sufficient for the silhouette.
- [ ] Abrupt density changes were reviewed.
- [ ] Long, thin triangles were reviewed.
- [ ] Narrow sliver faces were reviewed.
- [ ] Uncontrolled n-gons were reviewed.
- [ ] Poles are placed intentionally.
- [ ] Edge loops terminate intentionally.
- [ ] Topology does not merely conceal intersecting primitives.
- [ ] There are no accidental stacked faces.
- [ ] Geometry is suitable for the stated downstream use.

### Quad requirements

When quads are required:

- [ ] Deforming and subdivided areas primarily use quads.
- [ ] Quad flow supports expected deformation.
- [ ] Quads are not excessively skewed.
- [ ] Quad size is reasonably consistent.
- [ ] Triangles and n-gons are limited to appropriate areas.

### Game-ready requirements

When intended for real-time use:

- [ ] Polygon budget is defined.
- [ ] Polygon count is within budget.
- [ ] Hidden or unnecessary faces were removed where appropriate.
- [ ] Silhouette quality was prioritized over invisible density.
- [ ] LOD requirements were considered.
- [ ] Triangulation behavior was inspected.
- [ ] Export triangulation will not alter the visible result unexpectedly.

Record:

```text
Vertex count:
Edge count:
Face count:
Triangle count:
```

---

## 8. Modifier stack

- [ ] Modifier order was reviewed.
- [ ] Every modifier has a clear purpose.
- [ ] Unused modifiers were removed.
- [ ] Modifier names are meaningful when multiple similar modifiers exist.
- [ ] Modifier viewport and render settings are appropriate.
- [ ] Modifier dependency on object scale was checked.
- [ ] Modifier dependency on other objects was checked.
- [ ] Missing modifier target objects were checked.
- [ ] Final export behavior was considered.
- [ ] Modifiers that must remain editable were not applied unnecessarily.
- [ ] Modifiers that must be applied for export were applied in the export copy.

### Mirror

- [ ] Mirror plane is correct.
- [ ] Object origin supports the intended mirror plane.
- [ ] Merge is enabled when appropriate.
- [ ] Center vertices merge correctly.
- [ ] No center seam remains.
- [ ] Clipping behavior is correct.
- [ ] Symmetrical geometry is actually symmetrical.
- [ ] Intended asymmetry was preserved.

### Subdivision Surface

- [ ] Base cage was inspected.
- [ ] Subdivided result was inspected.
- [ ] Silhouette does not collapse.
- [ ] Support loops are intentional.
- [ ] Pinching was checked.
- [ ] Corners retain intended sharpness.
- [ ] Subdivision level is appropriate.
- [ ] Render level is not excessive.
- [ ] Boundary behavior is correct.

### Boolean

- [ ] Boolean operation mode is appropriate.
- [ ] Cutter geometry is valid.
- [ ] Result contains no unexpected holes.
- [ ] Internal faces were removed.
- [ ] Coplanar overlap issues were checked.
- [ ] Long thin faces were checked.
- [ ] Normals were checked after Boolean.
- [ ] Shading was checked after Boolean.
- [ ] Topology was cleaned where necessary.

### Shrinkwrap

- [ ] Target object is correct.
- [ ] Projection direction is correct.
- [ ] Offset is appropriate.
- [ ] No unwanted penetration exists.
- [ ] No unwanted floating areas exist.
- [ ] Projection does not jump across nearby surfaces.
- [ ] Result was inspected during expected deformation.

### Solidify

- [ ] Thickness is appropriate.
- [ ] Thickness direction is correct.
- [ ] Rim behavior is correct.
- [ ] Corners do not self-intersect.
- [ ] Thickness is visually consistent.
- [ ] Even Thickness was evaluated.
- [ ] Normals remain correct.

---

## 9. Hard-surface model checks

Use when applicable.

- [ ] Large planar surfaces are actually planar.
- [ ] Intended curved surfaces are smooth.
- [ ] Bevel width is consistent.
- [ ] Bevel segment count is appropriate.
- [ ] Edge sharpness matches the reference.
- [ ] Mechanical transitions are intentional.
- [ ] Repeated elements are consistently spaced.
- [ ] Openings and cutouts have clean borders.
- [ ] Boolean cuts were cleaned.
- [ ] No accidental dents exist on planar surfaces.
- [ ] Panel gaps and seams have consistent depth.
- [ ] Small details do not distort the primary silhouette unnecessarily.

---

## 10. Organic model checks

Use when applicable.

- [ ] Large anatomical or organic masses are established.
- [ ] The model does not visibly retain sphere or capsule construction.
- [ ] Surface transitions are continuous.
- [ ] Volume is preserved across major forms.
- [ ] Left-right symmetry is appropriate.
- [ ] Intended asymmetry is present where required.
- [ ] Thin regions do not collapse.
- [ ] Sculpted detail does not conceal incorrect proportions.
- [ ] Secondary forms support the primary silhouette.
- [ ] Surface noise is controlled.
- [ ] Retopology follows major form direction.
- [ ] Deformation zones have sufficient topology.

---

## 11. Clothing and fitted asset checks

Use when applicable.

- [ ] Clothing fits the target body.
- [ ] Required body clearance is present.
- [ ] Clothing does not penetrate the body in the neutral pose.
- [ ] Clothing does not float excessively above the body.
- [ ] Thickness is appropriate.
- [ ] Seams are placed intentionally.
- [ ] Openings have clean boundaries.
- [ ] Sleeves, collars, waistlines, and hems align correctly.
- [ ] Shrinkwrap offset was checked.
- [ ] Solidify thickness was checked.
- [ ] Folds support the garment structure.
- [ ] Folds do not resemble random surface noise.
- [ ] Deformation was tested at major joints.
- [ ] Elbow, shoulder, hip, and knee regions have suitable edge flow.
- [ ] Mirrored geometry does not create an unwanted center seam.
- [ ] Hidden body geometry removal was considered where appropriate.

---

## 12. Rigging and deformation checks

Use when applicable.

- [ ] Armature scale and transforms were checked.
- [ ] Mesh and armature origins align appropriately.
- [ ] Parenting is correct.
- [ ] Vertex groups are named correctly.
- [ ] Unweighted vertices were checked.
- [ ] Multiply weighted problem areas were checked.
- [ ] Weight normalization was checked.
- [ ] Left-right weight symmetry was checked where appropriate.
- [ ] Shoulder deformation was tested.
- [ ] Elbow deformation was tested.
- [ ] Wrist deformation was tested.
- [ ] Hip deformation was tested.
- [ ] Knee deformation was tested.
- [ ] Neck deformation was tested.
- [ ] Extreme test poses were inspected.
- [ ] Volume loss was reviewed.
- [ ] Mesh intersections during deformation were reviewed.
- [ ] Corrective shape keys were considered where necessary.

---

## 13. UV checks

Use when applicable.

- [ ] UV map exists.
- [ ] UV map has a meaningful name.
- [ ] Required seams are marked.
- [ ] UV islands correspond logically to model regions.
- [ ] UV islands are not unintentionally overlapping.
- [ ] Intentional overlaps are documented.
- [ ] Texel density is reasonably consistent.
- [ ] Important visible areas receive sufficient UV space.
- [ ] UV stretching was inspected.
- [ ] Checker texture was inspected.
- [ ] Mirrored UV decisions are intentional.
- [ ] Padding is sufficient for the target texture resolution.
- [ ] UVs remain inside the expected tile or UDIM range.
- [ ] Exported UV orientation is correct.

---

## 14. Materials and textures

Use when applicable.

- [ ] Materials have meaningful names.
- [ ] Material slots are intentional.
- [ ] Unused material slots were removed.
- [ ] Every required face has the correct material.
- [ ] Missing textures were checked.
- [ ] Texture color space settings are correct.
- [ ] Normal map settings are correct.
- [ ] Alpha mode is correct.
- [ ] Backface behavior is correct.
- [ ] Materials render correctly in the target renderer.
- [ ] Material appearance was checked under neutral lighting.
- [ ] Texture paths are portable or packed as required.

---

## 15. Sculpt and remesh checks

Use when applicable.

- [ ] Sculpt resolution is appropriate.
- [ ] Voxel size is documented.
- [ ] Voxel remesh did not erase important features.
- [ ] Surface noise is controlled.
- [ ] Dynamic topology artifacts were checked.
- [ ] Thin surfaces were not accidentally merged.
- [ ] Separate nearby forms were not unintentionally fused.
- [ ] Retopology was performed when required.
- [ ] The sculpted mesh is not being used directly when unsuitable for export.
- [ ] High-poly and low-poly versions are clearly separated.

---

## 16. Geometry Nodes checks

Use when applicable.

- [ ] Node group has a meaningful name.
- [ ] Exposed parameters have meaningful names.
- [ ] Parameter ranges are sensible.
- [ ] Generated geometry is stable across parameter ranges.
- [ ] Realized Instances behavior was considered.
- [ ] Normals are correct.
- [ ] Generated geometry is manifold where required.
- [ ] Excessive geometry generation was checked.
- [ ] Dependencies on external objects are documented.
- [ ] Node group inputs are suitable for reuse.
- [ ] Export behavior was tested or documented.

---

## 17. Rendering and visual inspection

Use consistent inspection settings.

- [ ] Neutral material or clay render inspected.
- [ ] Wireframe overlay inspected.
- [ ] Face orientation inspected.
- [ ] Front render saved.
- [ ] Side render saved.
- [ ] Rear render saved when relevant.
- [ ] Perspective render saved.
- [ ] Close-up render saved for critical details.
- [ ] Lighting does not conceal surface problems.
- [ ] Camera focal length does not excessively distort the model.
- [ ] All comparison renders use consistent framing where possible.
- [ ] Validation images correspond to the final saved model.

Expected files:

```text
blender/renders/front.png
blender/renders/side.png
blender/renders/back.png
blender/renders/perspective.png
blender/renders/wireframe.png
blender/renders/face-orientation.png
```

---

## 18. Save and reproducibility checks

- [ ] A blockout checkpoint exists.
- [ ] A primary-form checkpoint exists.
- [ ] A topology or cleanup checkpoint exists.
- [ ] A final checkpoint exists.
- [ ] The only valid `.blend` file was not overwritten.
- [ ] Reusable scripts were saved.
- [ ] Script paths are documented.
- [ ] Scripts use stable object names.
- [ ] Scripts avoid unnecessary dependence on UI coordinates.
- [ ] Scripts explicitly establish active object and mode when required.
- [ ] Scripts handle existing generated objects safely.
- [ ] Generated collections or objects can be recreated deliberately.
- [ ] External dependencies are documented.
- [ ] The final `.blend` file opens without missing required data.
- [ ] The final asset can be regenerated or modified without starting over.

Expected files:

```text
blender/checkpoints/01_blockout.blend
blender/checkpoints/02_primary_forms.blend
blender/checkpoints/03_topology.blend
blender/checkpoints/04_final.blend
blender/scripts/
```

---

## 19. Export checks

Use when export is required.

- [ ] Target format is confirmed.
- [ ] Export scale is correct.
- [ ] Axis orientation is correct.
- [ ] Object transforms are correct.
- [ ] Required modifiers are applied in the export copy.
- [ ] Armature export settings are correct.
- [ ] Animation export settings are correct.
- [ ] Materials and textures are included as required.
- [ ] Unwanted objects are excluded.
- [ ] Triangulation behavior is correct.
- [ ] Shape keys are preserved where required.
- [ ] Vertex groups are preserved where required.
- [ ] UV maps are preserved.
- [ ] Normals and tangents are exported correctly.
- [ ] Exported file was imported into the target application for verification.
- [ ] Imported result visually matches the Blender source.
- [ ] File creation, re-import, scripted preview, and target-runtime behavior are reported as separate evidence levels.

---

## 20. Final completion gate

The model may be declared complete only when all applicable statements are true.

- [ ] The requested object is recognizable from silhouette alone.
- [ ] The major proportions are acceptable.
- [ ] The model is not merely an assembly of unchanged primitives.
- [ ] Required views were inspected.
- [ ] Mesh integrity was validated.
- [ ] Normals were validated.
- [ ] Topology is appropriate for the stated use.
- [ ] Modifier behavior was validated.
- [ ] Required deformation was tested.
- [ ] Required UV and material checks were completed.
- [ ] Final files were saved.
- [ ] Validation images were saved.
- [ ] Known limitations were documented.
- [ ] No unverified claim of success remains.
- [ ] Every required output has verification evidence; missing requirements are not relabeled as optional limitations.

---

## Final validation report template

```text
# Final Blender Validation Report

## Asset

Name:
Purpose:
Blender version:
Unit system:
Final file:

## Geometry statistics

Objects:
Vertices:
Edges:
Faces:
Triangles:

## Dimensions

Width:
Depth:
Height:

## Modifiers

- Object:
  - Modifier:
  - Status:

## Mesh validation

Duplicate vertices:
Loose vertices:
Loose edges:
Loose faces:
Non-manifold edges:
Disconnected islands:
Internal faces:
Normals checked:
Face orientation checked:

## Visual validation

Front view:
Side view:
Rear view:
Perspective view:
Wireframe view:

Largest remaining visual differences:

1.
2.
3.

## Downstream validation

Rig tested:
UV checked:
Materials checked:
Export tested:
Target application import tested:

## Output files

- Final blend:
- Checkpoints:
- Scripts:
- Validation renders:
- Exported assets:

## Known limitations

-
```
