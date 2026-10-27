# FACS Character Continuity

An [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) that keeps AI-generated characters consistent across images, camera angles, expressions, and short video scenes.

It treats a character's identity as a **locked baseline** and every expression as a **controlled, reversible delta** from that baseline, so a new scene can act without inventing a new face.

## What it does

- **Identity pack first** – guides you to a neutral multi-view reference set (front, ¾ left, ¾ right, profile) and a written record of locked features, with extra care for the mouth and lower face, where drift is most common.
- **Expressions as deltas** – directs brow, eyes, cheeks, mouth, gaze, and head separately, with an A–E intensity scale, symmetry, and onset → apex → hold → release timing for video.
- **Generator-ready prompts** – a fixed identity block plus only the scene-specific delta, usable with any image or video model.
- **Review gate** – separate `pass / review / fail / not_assessable` checks for identity, lower face, expression, intensity, pose, wardrobe, and (optionally) face-mesh and blendshape data, followed by a library decision: `adopt`, `restricted_use`, or `regenerate`.
- **Honest about evidence** – visual observations are labelled as visual observations, never presented as biometric measurement or formal FACS coding.

## Installation

### Claude (web, desktop, and mobile apps)

1. Download **[facs-character-continuity.zip](https://github.com/Cittasana/facs-character-continuity/releases/latest/download/facs-character-continuity.zip)** from the latest release.
2. Make sure code execution is on: **Settings → Capabilities → Code execution and file creation** (shown as *Create and edit files* in the newer layout). On Team and Enterprise plans, an owner may need to enable skills for the organization.
3. Open **Customize → Skills**, click **+ → Create skill → Upload a skill**, and select the ZIP.

Details: [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude)

### Claude Code (as a plugin)

```bash
/plugin marketplace add Cittasana/facs-character-continuity
/plugin install facs-character-continuity@cittasana-skills
```

Claude picks the skill up automatically when a request matches. You can also call it directly with `/facs-character-continuity:facs-character-continuity`.

### Claude Code (manual)

Copy the skill folder into your personal or project skills directory:

```bash
git clone https://github.com/Cittasana/facs-character-continuity.git
cp -r facs-character-continuity/skills/facs-character-continuity ~/.claude/skills/
# or, for one project only:
cp -r facs-character-continuity/skills/facs-character-continuity .claude/skills/
```

### Claude API and other agents

Upload the folder through the [Skills API](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview). Agents that follow the open Agent Skills format can load `skills/facs-character-continuity/` as it is.

## Worked example

[`examples/C-001-mara-kessling.md`](examples/C-001-mara-kessling.md) walks through one fictional character from start to finish: the locked identity pack, a still expression card ("holding it together"), a three-second video beat ("suppressed smile"), the generator-ready prompts for both, and three reviewed candidates that end in `regenerate`, `adopt`, and `restricted_use`.

## Example prompts

- *"Build an identity pack for my character Lena: a woman in her 30s with a small scar above the left eyebrow and a slightly lopsided resting smile."*
- *"Write an expression card for C-001: she has just heard bad news and is trying not to show it. Intensity B, natural asymmetry."*
- *"Give me a generator-ready prompt for a 4-second shot: three-quarter left, she suppresses a smile, release into neutral."*
- *"Review this candidate image against the neutral front reference and tell me whether to adopt, restrict, or regenerate it."*

## Repository layout

```
.
├── .claude-plugin/
│   ├── marketplace.json      # lets Claude Code install this repo as a plugin
│   └── plugin.json
├── skills/
│   └── facs-character-continuity/
│       ├── SKILL.md          # the skill itself
│       └── references/
│           └── expression-card-schema.md
├── examples/
│   └── C-001-mara-kessling.md   # full worked character card
├── .github/workflows/
│   └── release.yml           # builds the uploadable ZIP on every version tag
├── LICENSE
└── README.md
```

## Data and privacy

The skill is instructions only: two Markdown files, no scripts, no MCP servers, no hooks, and no network calls. It sends no data anywhere and collects nothing. Any images you work with stay in your Claude conversation and in whichever image or video generator you choose to use.

## Scope and responsible use

This skill is for designing **fictional or consenting characters** in creative production: character sheets, storyboards, short films, games, and similar work.

- Do not use it to reproduce a real person's likeness without their permission.
- It is not a tool for reading emotions, detecting lies, or making psychological or biometric claims about real people's faces. The skill itself refuses that framing.
- Check the terms of the image or video generator you use; many restrict depictions of real people.

## About FACS

The Facial Action Coding System was developed by Paul Ekman and Wallace V. Friesen (later revised with Joseph C. Hager). This project borrows the general idea of describing visible facial actions. It contains **no text, tables, images, or training material from the FACS manual**, is not a substitute for FACS training, and is not affiliated with or endorsed by the Paul Ekman Group. All trademarks belong to their respective owners.

## Contributing

Issues and pull requests are welcome, especially worked examples from real productions (with generated, not real-person, characters). Please keep the skill model-neutral and keep visual observations clearly separate from measurements.

## License

[MIT](LICENSE) © 2026 Cittasana S.R.L.
