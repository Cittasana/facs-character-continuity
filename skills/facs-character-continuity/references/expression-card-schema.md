# Expression-card and candidate-review schema

Use this as a compact, model-neutral production record. It distinguishes the intended performance from what is visible in a candidate. Translate it into the syntax required by the chosen image or video generator.

```yaml
character_id: C-001
baseline_set: C-001-neutral-v1
candidate_id: C-001-E07-v1

source_references:
  - id: C-001-neutral-front-v1
    role: neutral_front
  - id: C-001-neutral-three-quarter-left-v1
    role: neutral_angle_match

identity_lock:
  preserve:
    - facial geometry
    - eye and lid shape
    - hairline
    - skin texture
    - fixed marks
    - established asymmetries
  mouth_lower_face_neutral:
    mouth_width: "Visual relation to stable landmarks; no invented ratio"
    upper_lower_lip_visibility: "Neutral visible relationship"
    lip_contour_and_cupids_bow: "Visual description"
    philtrum: "Visual length and shape"
    mouth_corners_and_asymmetry: "Resting position and natural asymmetry"
    lower_lip_to_chin_spacing: "Visual spacing at neutral"
    chin_and_jaw_transition: "Visual shape and transition"
  do_not_change:
    - apparent age
    - facial proportions outside the requested expression
    - neutral mouth/lower-face geometry outside the requested expression

mesh_reference: # omit only when no mesh/tracker is used
  tracker: "Verified tracker and model version, e.g. MediaPipe Face Landmarker"
  topology: "478-landmark mesh | verified alternative topology and point count"
  neutral_view_reference: "Named landmark set for this matching approved view"
  capture_conditions: "Pose, crop, camera/perspective, and light of the neutral capture"
  face_pose_transform: "Recorded transform if supplied by the tracker; otherwise not_available"
  permitted_use: "Visual geometry and relative movement comparison only"
  prohibited_claims:
    - biometric identity measurement
    - anatomy scan
    - direct FACS Action Unit equivalence
    - emotion or truthfulness inference

blendshape_targets: # omit only when the tracker provides none
  source_model: "Verified model supplying the coefficients"
  requested:
    brow_forehead: "Expected direction or not_applicable; do not invent values"
    eyelids_eyes: "Expected direction or not_applicable; do not invent values"
    cheeks_nose: "Expected direction or not_applicable; do not invent values"
    mouth_lips_jaw: "Expected direction or not_applicable; do not invent values"
  observed:
    brow_forehead: "Observed direction/value and capture context"
    eyelids_eyes: "Observed direction/value and capture context"
    cheeks_nose: "Observed direction/value and capture context"
    mouth_lips_jaw: "Observed direction/value and capture context"
  interpretation_limit: "Visual-motion trace only; never a 1:1 FACS translation"

dramatic_beat:
  trigger: "What has just happened?"
  objective: "What does the character want in this moment?"
  subtext: "What are they concealing, resisting, or allowing?"
  emotional_read: "Audience-facing interpretation, not a diagnosis"

requested_expression:
  brow_forehead: {action: "Visible movement", target_intensity: "A-E or not_applicable"}
  eyelids_eyes: {action: "Visible movement and gaze", target_intensity: "A-E or not_applicable"}
  cheeks_nose: {action: "Visible movement", target_intensity: "A-E or not_applicable"}
  mouth_lips_jaw: {action: "Visible movement", target_intensity: "A-E or not_applicable"}
  symmetry: "bilateral | left-biased | right-biased | natural asymmetry"
  optional_facs_notation: "Only if independently verified; never notation alone"

observed_expression:
  brow_forehead: "What is actually visible"
  eyelids_eyes: "What is actually visible"
  cheeks_nose: "What is actually visible"
  mouth_lips_jaw: "What is actually visible"
  intensity_by_region: "Observed A-E where visually supportable, otherwise not_assessable"

body_camera_and_light:
  head_pose: "e.g. three-quarter left, chin slightly down"
  gaze: "e.g. just past camera to the right"
  shot_and_crop: "e.g. close-up, comparable crop to reference"
  perspective: "e.g. comparable lens/camera distance, or documented limitation"
  lighting: "e.g. neutral soft light, or documented limitation"

motion: # required for video; optional for a still
  onset: "How the expression begins"
  apex: "Shortest clear peak"
  hold: "Duration or none"
  release: "Return, masking action, or transition"

costume_and_props: # include when relevant
  layer_order: ["shirt", "vest", "jacket"]
  jacket_vest_openings_and_fasteners: "State opening, buttons, zip, etc."
  straps: "Path and visible placement"
  recurring_props: "Position, orientation, and handling"

comparability:
  head_pose: "comparable | limited | not_comparable"
  perspective: "comparable | limited | not_comparable"
  crop: "comparable | limited | not_comparable"
  lighting: "comparable | limited | not_comparable"
  limitations: ["Features hidden by angle, expression, shadow, or crop"]
  additional_reference_needed: false

review:
  assessment_basis: "visual_assist_review | human_approval | measurement"
  intended_changes: ["Requested changes, copied without post-hoc adjustment"]
  observed_differences: ["Visible differences from matching neutral reference"]
  not_assessable_features: ["Feature and reason"]
  checks:
    identity_match: {status: "pass | review | fail | not_assessable", reason: "Short reason"}
    mouth_lower_face_match: {status: "pass | review | fail | not_assessable", reason: "Short reason"}
    expression_match: {status: "pass | review | fail | not_assessable", reason: "Short reason"}
    expression_intensity_match: {status: "pass | review | fail | not_assessable", reason: "Short reason"}
    pose_camera_match: {status: "pass | review | fail | not_assessable", reason: "Short reason"}
    wardrobe_continuity: {status: "pass | review | fail | not_assessable", reason: "Use not_assessable if irrelevant or not visible"}
    mesh_geometry_match: {status: "pass | review | fail | not_assessable", reason: "Use not_assessable when no comparable mesh reference exists"}
    blendshape_target_match: {status: "pass | review | fail | not_assessable", reason: "Use not_assessable when no blendshape output or target exists"}
  allowed_use: "Specific scene, angle, costume, reference role, or no use"
  library_decision: "adopt | restricted_use | regenerate"
  decision_reason: "Why this use is or is not allowed"
```

## Decision rules

- `pass`, `review`, `fail`, and `not_assessable` apply to individual checks, never to `library_decision`.
- `adopt` is limited to the explicitly named role. An expression at intensity B is not automatically an apex reference for intensity C, and a costume-specific image is not a general costume reference.
- `restricted_use` allows only the stated scene, angle, costume, or purpose. It does not replace an established reference.
- `regenerate` is required when a required check fails. A candidate with `review` or `not_assessable` may only receive `restricted_use` after explicit human approval and documented limits; it cannot become canonical.
- Report visual descriptions as visual descriptions. Do not present them as biometric measurements or formal FACS coding unless those methods were actually used.
- Compare landmarks only with a named neutral mesh captured at a comparable pose, crop, perspective, and lighting. A mesh difference from unmatched views is a limitation, not evidence of identity drift.
- Treat blendshape values as tracker-specific motion signals. Compare requested and observed direction first; do not create numeric targets unless the production has validated them from its own approved references.

## Generator-ready prompt frame

Keep the identity wording unchanged. Replace only bracketed values:

```text
Use approved character [Character ID] and approved neutral references [baseline set].
Preserve facial geometry, eye and eyelid shape, hairline, skin texture, fixed marks,
natural asymmetries, neutral mouth width, lip contour and cupid's bow, philtrum,
mouth-corner position, lower-lip-to-chin relation, and chin-to-jaw transition.
Do not redesign the face or alter these features beyond the specified expression.

Scene: [dramatic beat and physical setting].
Requested expression delta: [plain-language visible action plan per region].
Target intensity per region: [targets]. Symmetry: [symmetry].
Gaze and head: [gaze/head pose]. [For video: onset → apex → hold/release.]
Camera and light: [shot, crop, perspective, lighting].
[When relevant: costume layers, fasteners, straps, and props.]
Avoid beauty retouching, a theatrical full-face grimace, accidental symmetry,
changed age, changed identity, or a different expression intensity.
```

## Filled example: controlled tension with slight lip pressing

```yaml
character_id: C-001
baseline_set: C-001-neutral-v1
candidate_id: C-001-E07-v1
source_references: [C-001-neutral-front-v1, C-001-neutral-three-quarter-left-v1]
requested_expression:
  brow_forehead: {action: "Brow remains close to neutral; slight central tension", target_intensity: "A"}
  eyelids_eyes: {action: "Focused gaze slightly past camera; lids subtly firmer", target_intensity: "A"}
  cheeks_nose: {action: "No requested change", target_intensity: "not_applicable"}
  mouth_lips_jaw: {action: "Lips meet with slight pressure; no corner pull; jaw remains closed", target_intensity: "A"}
  symmetry: "natural asymmetry"
observed_expression:
  brow_forehead: "Slight tension between the brows is visible."
  eyelids_eyes: "Focused gaze and slightly firmer lids are visible."
  cheeks_nose: "No clear change visible."
  mouth_lips_jaw: "Lips are gently pressed; the visible lip height is slightly reduced, consistent with the requested action."
  intensity_by_region: "brow A; lids A; mouth A"
comparability:
  head_pose: comparable
  perspective: comparable
  crop: comparable
  lighting: comparable
  limitations: []
  additional_reference_needed: false
review:
  assessment_basis: visual_assist_review
  intended_changes: ["Slight brow/lid tension", "slight lip pressing"]
  observed_differences: ["Reduced visible lip height from pressing", "no changed cupid's bow or mouth width visible"]
  not_assessable_features: []
  checks:
    identity_match: {status: pass, reason: "Stable geometry and identifying features match the neutral reference."}
    mouth_lower_face_match: {status: pass, reason: "The reduced visible lip height is explained by slight pressing; lower-face form remains consistent."}
    expression_match: {status: pass, reason: "The requested controlled tension is visible without an added smile or frown."}
    expression_intensity_match: {status: pass, reason: "All visible actions remain at the requested subtle A level."}
    pose_camera_match: {status: pass, reason: "Comparable frontal pose, crop, and neutral light."}
    wardrobe_continuity: {status: not_assessable, reason: "The crop does not show wardrobe."}
    mesh_geometry_match: {status: not_assessable, reason: "No comparable named mesh reference was supplied for this example."}
    blendshape_target_match: {status: not_assessable, reason: "No tracker output was supplied for this example."}
  allowed_use: "C-001 controlled-tension still, frontal or closely matching angle"
  library_decision: adopt
  decision_reason: "Adopt only as the named subtle-intensity expression variant; not as a stronger apex reference."
```
