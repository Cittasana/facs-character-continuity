---
name: facs-character-continuity
description: Create and use a FACS-informed character reference system for consistent AI-generated character images and short video scenes. Use when building a character sheet, expression library, turnaround, or scene prompt where a character's face and identity must stay consistent across shots, angles, and expressions.
license: MIT
---

# FACS Character Continuity

Treat character identity as a locked baseline and expression as a controlled, reversible deviation from it. The goal is believable screen acting without letting a new scene invent a new face.

## Scope and boundary

Use this skill to design reference packs, expression libraries, and generation briefs. It is not a tool for inferring a person's hidden emotions, diagnosing truthfulness, or making psychological claims from their face.

FACS describes visible facial actions; an emotion is a dramatic interpretation supplied by context. Keep those two layers separate. Do not reproduce copyrighted FACS manual text, tables, images, or training examples. Describe actions independently and in original language.

## Build the identity pack first

Before generating emotional variants, establish a `Character ID` and a neutral reference set. Capture or generate the same adult character in neutral expression, consistent styling, and at least front, three-quarter left, three-quarter right, and profile views. Use clean, even light; do not use an extreme lens, heavy smile, theatrical makeup, strong shadow, or a speaking pose as the baseline.

Document two classes of attributes from the neutral references:

- **Locked identity:** facial proportions, eye and lid geometry, brow placement, nose and jaw shape, lip shape, hairline, skin tone and texture, fixed marks, apparent age range, and natural asymmetries. For the mouth and lower face, explicitly record mouth width relative to stable facial landmarks; the neutral visible upper-to-lower-lip relationship; lip contour and cupid's bow; philtrum length and shape; resting mouth-corner position and natural asymmetry; lower-lip-to-chin spacing; and chin shape and transition into the jaw.
- **Flexible scene state:** expression, eye direction, head pose, lighting, wardrobe, grooming, makeup, camera, and background.

Describe these features visually unless they were actually measured from suitable source material. Do not invent dimensions, ratios, thresholds, or biometric precision. A visual observation such as “the lower lip is visibly fuller than the upper lip at rest” is not a measurement.

Include a concise no-change instruction with every generation brief: preserve the locked identity and do not alter age, facial proportions, eye shape, hairline, skin texture, distinguishing marks, or the neutral mouth/lower-face geometry beyond the specified expression delta.

A 3D face mesh or a multi-view reconstruction is useful as a geometry anchor when it accurately represents the approved character. It complements, but never replaces, the approved image references. Do not introduce a mesh-derived image into the canonical reference set until its identity match has been approved.

When the selected tracker provides a 478-landmark face mesh, store a named neutral landmark reference for every approved view together with its capture conditions and face-pose transform. Use the mesh to compare visible geometry and relative movement within comparable views; it is not a biometric identity measurement, a precise anatomy scan, or a universal coordinate set across camera angles. If a different tracker/topology is used, record its verified name and actual point count rather than calling it “478 points”.

If available, use blendshape coefficients as a separate visual-motion trace: record the requested directional targets for the relevant regions, the observed values or directions, and their source model. Do not invent target numbers. A blendshape is not equivalent to a FACS Action Unit, and a coefficient alone cannot prove an expression, emotion, or identity match. Resolve a disagreement between mesh, blendshape, and visible reference by assigning `review` or `not_assessable` and obtaining a better-matched reference or human approval.

## Direct an expression as a delta

Write expression direction as a delta from the approved neutral baseline, not as a replacement face. Use this order:

1. **Dramatic beat:** event, objective, subtext, and whether the emotion is expressed, restrained, masked, or involuntary.
2. **Visible action plan:** separately direct brow/forehead, eyelids/eyes, cheeks/nose, mouth/lips/jaw, gaze, and head.
3. **Strength:** rate each action from A (barely detectable) to E (near maximum). Prefer A-C unless the script genuinely needs an extreme expression.
4. **Spatial character:** bilateral, deliberately one-sided, or naturally asymmetric. Preserve the character's established resting asymmetry. For a one-sided action, name the side by a visible landmark from the identity pack (for example "the side without the mole") and also state the image side, because generators often confuse the character's left and right with the image's left and right. Check the side again in review.
5. **Time:** for motion, specify onset, apex, hold, and release. A microexpression is a brief event in motion; do not describe a static portrait as one.

Set a requested action and target intensity for each relevant facial region before generating. Then separately document what is actually visible in each output. Do not reinterpret a missed target as a pass by rewriting the intended action after the fact.

An instructed action can legitimately change visible proportions: for example, lip pressing can reduce visible lip height, an open jaw can change lower-lip-to-chin spacing in projection, and a smile can move mouth corners. Treat those as expression changes only when their direction and degree are plausibly explained by the approved action plan. Check for drift when lip contour, resting mouth width, cupid's bow, philtrum, chin/jaw geometry, or established asymmetry changes beyond the instructed movement. If the cause cannot be determined, assign `review` or `not_assessable`, never a confident pass.

Use the FACS action notation only where it makes the brief clearer and it has been independently verified. Pair it with plain-language visible direction, as image and video generators do not reliably honor AU labels alone. Consult [the expression-card schema](references/expression-card-schema.md) whenever creating a reusable card or production brief.

## Generation workflow

1. Select the approved baseline views required by the shot angle.
2. Select one approved expression card or create a new provisional one from the schema.
3. Generate a controlled expression turn-around before using an untested expression in a dramatic scene. Each view in an expression series must target the same regional actions and comparable intensity.
4. Use the same approved references and fixed character wording in every scene. Add only the expression delta and scene-specific variables.
5. Curate: promote a generated image into the reference library only after identity review. Never let an unreviewed output become a new source of truth.

Compare identity and proportions under comparable conditions: similar head pose, camera perspective, crop, and neutral or equivalent lighting. Do not judge different views using unchecked two-dimensional width ratios or raw landmarks from unmatched poses. Record perspective or visibility limitations and obtain an additional matching-angle reference when the feature cannot be assessed.

If a view in an expression series is visibly weaker or stronger than the others, regenerate it or label it as a distinct intensity variant. Do not use different intensity variants as the same apex reference or as directly matching reverse shots.

For a video beat, use the neutral baseline and approved apex as anchors when the generator supports multiple references. Direct the temporal path rather than independently generating unrelated frames.

## Costume and prop continuity

For a scene reference, document layer order; jacket and vest opening and fasteners; strap paths; and the position and handling of recurring props. An image with changed costume or prop continuity is not a silent replacement for the established costume reference. Assess wardrobe continuity only when it is relevant and sufficiently visible; otherwise use `not_assessable`.

## Identity review gate

Review every candidate before delivery or library promotion. Record the source references, requested changes, observed differences, and unassessable features. Mark the basis of each assessment as visual-assist review, human approval, or actual measurement. Do not claim biometric accuracy or formal FACS coding without a suitable method and evidence.

Give separate results, each with a status (`pass`, `review`, `fail`, or `not_assessable`) and a short reason: identity match, mouth/lower-face match, expression match, expression-intensity match, pose/camera match, wardrobe continuity when relevant, and mesh-geometry plus blendshape-target match when a mesh is in use. A pass for identity does not pass the expression, mesh, or wardrobe. A `not_assessable` result is not evidence of a pass.

Regenerate when a locked feature has drifted, including changed eye/lid shape, inter-feature spacing, nose or jaw geometry, hairline, skin texture, fixed mark, age impression, or a reversed established asymmetry. Also regenerate when the expression needs impossible-looking tension, changes the character's face more than the action plan warrants, becomes unintentionally symmetrical, or fails the requested intensity.

Separate the results:

- **Adopt:** suitable for its explicitly stated library role only (for example, canonical neutral baseline or named expression/intensity variant).
- **Restricted use:** suitable only for the named scene, angle, costume, or purpose; it is not a general reference.
- **Regenerate:** not approved for the stated purpose.

The library decision is independent of the individual checks. Do not promote a candidate to a canonical reference when any required check is `review`, `fail`, or `not_assessable`. A human can explicitly accept restricted use with documented limitations, but that does not create a general approval.

If the input contains only one character portrait, say that consistency can improve but cannot be reliably locked across every angle; request or create the missing neutral multi-view pack before promising continuity.

## Deliverable format

When the user asks for a character-sheet entry or generation prompt, return:

1. Character ID and selected baseline references.
2. Locked identity summary and no-change rules.
3. Expression card: dramatic beat, visible action plan, intensity, symmetry, gaze/head direction, and timing when applicable.
4. A compact generator-ready prompt that preserves the baseline and adds only the delta.
5. The candidate protocol: inputs, intended and observed changes, limitations, individual checks with evidence basis, allowed use, and library decision.
