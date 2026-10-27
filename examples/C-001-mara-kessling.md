# Example character card: C-001 "Mara Kessling"

A complete, worked example of what the skill produces for one fictional character: the identity pack, two expression cards (a still and a short video beat), generator-ready prompts, and candidate reviews that end in each of the three library decisions.

> Mara Kessling is an invented character for a fictional short drama. Image IDs such as `C-001-neutral-front-v1` are placeholders for your own approved files; no images are included. All observations below are written as a reviewer would record them and are visual descriptions, not measurements.

---

## 1. Character ID and baseline references

```yaml
character_id: C-001
display_name: Mara Kessling
project: "The Harbour Letters (fictional short drama)"
baseline_set: C-001-neutral-v1
baseline_status: approved            # human_approval, all four views
baseline_views:
  - id: C-001-neutral-front-v1
    role: neutral_front
  - id: C-001-neutral-three-quarter-left-v1
    role: neutral_angle_match
  - id: C-001-neutral-three-quarter-right-v1
    role: neutral_angle_match
  - id: C-001-neutral-profile-left-v1
    role: neutral_profile
baseline_capture: "Neutral expression, mouth closed, soft even frontal light, mid-grey background, no makeup beyond a natural base, hair tucked behind the ears"
```

## 2. Locked identity and no-change rules

```yaml
identity_lock:
  apparent_age: "Early 30s"
  face_shape: "Long oval face, high cheekbones, narrow chin"
  eyes_and_lids: "Almond-shaped, dark brown irises, slightly hooded upper lids; the left upper lid sits marginally lower than the right at rest"
  brows: "Straight, medium thickness, tapering at the outer ends; the right brow sits marginally higher"
  nose: "Straight, narrow bridge with a softly rounded tip"
  hair_and_hairline: "Dark brown, shoulder length, centre part, slight widow's peak"
  skin: "Light olive tone, fine texture, faint freckles across the nose bridge"
  fixed_marks:
    - "Small mole just below the outer corner of the right eye"
    - "Thin pale scar crossing the outer third of the left eyebrow"
  established_asymmetries:
    - "Left upper lid marginally lower"
    - "Right brow marginally higher"
    - "Right mouth corner sits marginally higher at rest"
  mouth_lower_face_neutral:
    mouth_width: "In the front view the mouth corners sit roughly below the inner edges of the irises"
    upper_lower_lip_visibility: "Both lips visible; upper lip visibly thinner than the lower lip"
    lip_contour_and_cupids_bow: "Defined cupid's bow with soft, rounded peaks; clear lower-lip contour"
    philtrum: "Medium length with a shallow groove"
    mouth_corners_and_asymmetry: "Corners neutral, neither up nor down; right corner marginally higher"
    lower_lip_to_chin_spacing: "Moderate; the chin reads as clearly separate from the lower lip"
    chin_and_jaw_transition: "Narrow, slightly pointed chin; soft transition into a defined jawline"
  do_not_change:
    - apparent age
    - facial proportions outside the requested expression
    - eye and lid shape, brow placement, nose, hairline, skin texture
    - mole and scar position
    - neutral mouth/lower-face geometry outside the requested expression
    - direction of every established asymmetry

flexible_scene_state: [expression, gaze, head pose, lighting, wardrobe, grooming, makeup, camera, background]
```

**No-change instruction used in every brief:**
Preserve the locked identity of C-001. Do not alter age, facial proportions, eye or lid shape, brow placement, nose, hairline, skin texture, the mole below the right eye, the scar through the left eyebrow, the established asymmetries, or the neutral mouth and lower-face geometry beyond the specified expression delta.

---

## 3. Expression card E03: "Holding it together" (still)

```yaml
expression_card: C-001-E03
type: still
dramatic_beat:
  trigger: "She has just read the letter confirming her brother's ship was lost."
  objective: "Not to break down in front of her colleague."
  subtext: "Grief is real and close; she is actively restraining it."
  mode: restrained
  emotional_read: "Contained grief (audience-facing interpretation, not a diagnosis)"

requested_expression:
  brow_forehead: {action: "Inner brow corners raise slightly and draw together; faint central forehead tension", target_intensity: "B"}
  eyelids_eyes: {action: "Upper lids lower slightly, lower lids tense; gaze down at the letter", target_intensity: "B"}
  cheeks_nose: {action: "No requested change", target_intensity: "not_applicable"}
  mouth_lips_jaw: {action: "Lips meet with light pressure; corners pull slightly down; slight chin raise; jaw closed", target_intensity: "B"}
  symmetry: "natural asymmetry (keep right mouth corner marginally higher)"

body_camera_and_light:
  head_pose: "Three-quarter left, chin slightly down"
  gaze: "Down to the letter held at chest height"
  shot_and_crop: "Medium close-up, head and shoulders"
  perspective: "Normal lens look, comparable camera distance to the three-quarter baseline"
  lighting: "Soft window light from frame left (scene lighting; differs from the baseline)"

costume_and_props:
  layer_order: ["cream blouse", "charcoal wool coat"]
  jacket_vest_openings_and_fasteners: "Coat closed with the lower two of three buttons; top button open; collar turned up"
  straps: "Brown leather satchel strap over the right shoulder, crossing to the left hip"
  recurring_props: "Folded letter held in both hands at chest height, fold line vertical"
```

**Generator-ready prompt (E03):**

```text
Use approved character C-001 and approved neutral references C-001-neutral-v1.
Preserve facial geometry, eye and eyelid shape, hairline, skin texture, fixed marks,
natural asymmetries, neutral mouth width, lip contour and cupid's bow, philtrum,
mouth-corner position, lower-lip-to-chin relation, and chin-to-jaw transition.
Do not redesign the face or alter these features beyond the specified expression.

Scene: a harbour office at dusk; she has just read a letter with bad news and is
holding herself together in front of a colleague.
Requested expression delta: inner brow corners slightly raised and drawn together;
upper lids slightly lowered, lower lids tense; lips meet with light pressure,
corners pulled slightly down, slight chin raise, jaw closed. No change to cheeks or nose.
Target intensity per region: brow B, eyes B, mouth B. Symmetry: natural asymmetry,
right mouth corner marginally higher.
Gaze and head: three-quarter left, chin slightly down, gaze down to the letter.
Camera and light: medium close-up, normal lens look, soft window light from frame left.
Costume and props: cream blouse under a charcoal wool coat, lower two of three buttons
closed, collar up; brown leather satchel strap over the right shoulder to the left hip;
folded letter held in both hands at chest height.
Avoid beauty retouching, a theatrical full-face grimace, accidental symmetry,
changed age, changed identity, or a different expression intensity.
```

---

## 4. Expression card E05: "Suppressed smile" (video beat)

```yaml
expression_card: C-001-E05
type: video_beat
duration: "about 3 seconds"
dramatic_beat:
  trigger: "During a tense meeting, a colleague makes a dry joke only she understands."
  objective: "Not to laugh in front of the harbour master."
  subtext: "Genuine amusement, masked within a second."
  mode: masked
  emotional_read: "Amusement she hides (audience-facing interpretation)"

requested_expression:
  brow_forehead: {action: "No requested change", target_intensity: "not_applicable"}
  eyelids_eyes: {action: "Lower lids lift slightly at the apex; gaze then drops down-right", target_intensity: "A"}
  cheeks_nose: {action: "Slight cheek lift at the apex", target_intensity: "A"}
  mouth_lips_jaw: {action: "Mouth corners pull up and back, right side first; then lips press together to mask it", target_intensity: "B"}
  symmetry: "right-biased onset, then natural asymmetry"

motion:
  onset: "0.0-0.3 s: right mouth corner begins to lift, left follows"
  apex: "0.3-0.8 s: brief visible smile with slight cheek lift"
  hold: "0.8-1.2 s"
  release: "1.2-2.0 s: lips press together and the smile flattens; gaze drops down-right; near-neutral by about 2.5 s"

body_camera_and_light:
  head_pose: "Front view, very slight turn to frame right"
  gaze: "Starts at the colleague just off camera left, ends down-right"
  shot_and_crop: "Close-up"
  perspective: "Comparable to the front baseline"
  lighting: "Overhead practical lamp plus soft fill (scene lighting)"

anchors: ["C-001-neutral-front-v1", "approved E05 apex still, once one exists"]
```

**Generator-ready prompt (E05):**

```text
Use approved character C-001 and approved neutral references C-001-neutral-v1.
Preserve facial geometry, eye and eyelid shape, hairline, skin texture, fixed marks,
natural asymmetries, neutral mouth width, lip contour and cupid's bow, philtrum,
mouth-corner position, lower-lip-to-chin relation, and chin-to-jaw transition.
Do not redesign the face or alter these features beyond the specified expression.

Scene: a tense meeting in a harbour office; a colleague makes a dry joke and she
must not laugh.
Requested expression delta: mouth corners pull up and back, right side first, with a
slight cheek lift and slightly lifted lower lids; then the lips press together to
hide the smile and the gaze drops down-right. Brows stay neutral.
Target intensity per region: mouth B, cheeks A, eyes A. Symmetry: right-biased onset,
then natural asymmetry.
Gaze and head: front view with a very slight turn to frame right; gaze starts just
off camera left, ends down-right.
Timing: onset 0.0-0.3 s, apex 0.3-0.8 s, hold to 1.2 s, release into a lip press by
2.0 s, near-neutral by 2.5 s.
Camera and light: close-up, perspective comparable to the front baseline, overhead
practical lamp with soft fill.
Avoid beauty retouching, a theatrical full-face grimace, accidental symmetry,
changed age, changed identity, or a different expression intensity.
```

---

## 5. Candidate reviews

Three reviewed candidates, one for each library decision. No face mesh or tracker was used for this character, so mesh and blendshape checks are not required and are recorded as `not_assessable`.

### C-001-E03-v1: regenerate

```yaml
candidate_id: C-001-E03-v1
source_references: [C-001-neutral-three-quarter-left-v1]
comparability:
  head_pose: comparable
  perspective: comparable
  crop: comparable
  lighting: limited
  limitations: ["Window light differs from the baseline; shadow side is the right cheek"]
  additional_reference_needed: false
observed_expression:
  brow_forehead: "Inner corners strongly raised and drawn together; clear horizontal forehead lines"
  eyelids_eyes: "Lids lowered, gaze on the letter"
  cheeks_nose: "No clear change"
  mouth_lips_jaw: "Lips pressed, corners down; the lips look fuller than at neutral and the cupid's bow is flattened; the left corner now sits higher than the right"
  intensity_by_region: "brow C; eyes B; mouth B"
review:
  assessment_basis: visual_assist_review
  intended_changes: ["Inner brow raise B", "lid lowering B", "lip press with corners down B, slight chin raise"]
  observed_differences: ["Brow stronger than requested", "fuller lips and flattened cupid's bow beyond what a light press explains", "mouth-corner asymmetry reversed"]
  not_assessable_features: []
  checks:
    identity_match: {status: review, reason: "Eyes, nose, marks and hairline match; lower-face drift makes the overall identity uncertain"}
    mouth_lower_face_match: {status: fail, reason: "Cupid's bow flattened and asymmetry reversed; not explained by a light lip press"}
    expression_match: {status: pass, reason: "Restrained grief reads as intended"}
    expression_intensity_match: {status: fail, reason: "Brow at C instead of B"}
    pose_camera_match: {status: pass, reason: "Three-quarter left, comparable crop and distance"}
    wardrobe_continuity: {status: pass, reason: "Coat buttons, collar, strap and letter as documented"}
    mesh_geometry_match: {status: not_assessable, reason: "No mesh in use for this character"}
    blendshape_target_match: {status: not_assessable, reason: "No tracker output"}
  allowed_use: "No use"
  library_decision: regenerate
  decision_reason: "A locked lower-face feature drifted and the brow intensity missed its target."
```

### C-001-E03-v2: adopt (named role only)

```yaml
candidate_id: C-001-E03-v2
source_references: [C-001-neutral-three-quarter-left-v1]
comparability:
  head_pose: comparable
  perspective: comparable
  crop: comparable
  lighting: limited
  limitations: ["Scene window light; right cheek in soft shadow, mole still visible"]
  additional_reference_needed: false
observed_expression:
  brow_forehead: "Inner corners slightly raised and drawn together; faint central tension"
  eyelids_eyes: "Upper lids slightly lowered, lower lids tense, gaze on the letter"
  cheeks_nose: "No clear change"
  mouth_lips_jaw: "Light lip press; visible lip height slightly reduced; corners slightly down; slight chin raise; right corner still marginally higher"
  intensity_by_region: "brow B; eyes B; mouth B"
review:
  assessment_basis: human_approval
  intended_changes: ["Inner brow raise B", "lid lowering B", "lip press with corners down B, slight chin raise"]
  observed_differences: ["Reduced visible lip height from the press", "slight chin raise", "no change to cupid's bow, mouth width or asymmetry visible"]
  not_assessable_features: []
  checks:
    identity_match: {status: pass, reason: "Geometry, marks, hairline and asymmetries match the three-quarter baseline"}
    mouth_lower_face_match: {status: pass, reason: "Changes are explained by the requested press and chin raise"}
    expression_match: {status: pass, reason: "Restrained grief, no added frown or grimace"}
    expression_intensity_match: {status: pass, reason: "All regions at B"}
    pose_camera_match: {status: pass, reason: "Comparable pose and crop; lighting difference recorded as a limitation"}
    wardrobe_continuity: {status: pass, reason: "Matches the E03 costume record"}
    mesh_geometry_match: {status: not_assessable, reason: "No mesh in use for this character"}
    blendshape_target_match: {status: not_assessable, reason: "No tracker output"}
  allowed_use: "C-001-E03 restrained grief, intensity B, three-quarter left, harbour-letter costume"
  library_decision: adopt
  decision_reason: "Adopted only as the named E03 variant. Not a general costume reference and not an apex reference for stronger grief."
```

### C-001-E05-v1: restricted use

```yaml
candidate_id: C-001-E05-v1
source_references: [C-001-neutral-front-v1]
comparability:
  head_pose: comparable
  perspective: comparable
  crop: comparable
  lighting: limited
  limitations: ["Overhead practical light; upper lids partly shadowed during the apex"]
  additional_reference_needed: false
observed_expression:
  brow_forehead: "Neutral"
  eyelids_eyes: "Slight lower-lid lift at the apex is hard to judge under the shadow; gaze drop present"
  cheeks_nose: "Slight cheek lift at the apex"
  mouth_lips_jaw: "Right-first smile onset reads well; release into a lip press happens at about 1.4 s instead of 1.2-2.0 s and is abrupt"
  intensity_by_region: "mouth B; cheeks A; eyes not_assessable"
motion_observed:
  onset: "As requested"
  apex: "As requested"
  hold: "Shorter than requested"
  release: "Too fast; lips snap shut"
review:
  assessment_basis: human_approval
  intended_changes: ["Right-first smile B", "cheek lift A", "lower-lid lift A", "masked release by 2.0 s, gaze down-right"]
  observed_differences: ["Hold shortened", "release abrupt", "lower-lid lift not judgeable"]
  not_assessable_features: ["Lower lids during the apex: shadowed by the overhead light"]
  checks:
    identity_match: {status: pass, reason: "Face, marks and asymmetries stable across the clip"}
    mouth_lower_face_match: {status: pass, reason: "Lower-face changes explained by the smile and press"}
    expression_match: {status: review, reason: "Onset and apex as requested; the release does not read as a controlled mask"}
    expression_intensity_match: {status: pass, reason: "Mouth B, cheeks A; eyes not judgeable"}
    pose_camera_match: {status: pass, reason: "Comparable front view and crop"}
    wardrobe_continuity: {status: not_assessable, reason: "Close-up does not show the costume"}
    mesh_geometry_match: {status: not_assessable, reason: "No mesh in use for this character"}
    blendshape_target_match: {status: not_assessable, reason: "No tracker output"}
  allowed_use: "Scene 12, shot 4 only, trimmed to 0.0-1.3 s and cut to the reverse shot before the release"
  library_decision: restricted_use
  decision_reason: "A human approved the trimmed onset and apex for this one cut. The clip is not an E05 reference and does not replace a full regeneration of the beat."
```
