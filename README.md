# presentation-craft

A Claude Code plugin for technical presentations and explainer videos that feel authored rather than generated.

`/presentation-craft` guides the agent through a three-stage workflow:

1. **Agree the story**: audience, single takeaway, honest starting state, and real proof artifacts.
2. **Design how to tell it**: pick one of five distinct visual styles and invent one or two novel visual moments (spatial metaphors, in-place artifact transformations, or live-workspace reveals).
3. **Build and verify**: deliver either a single self-contained offline 16:9 HTML deck or a deterministic 1920x1080 MP4 video rendered locally with [HyperFrames](https://www.npmjs.com/package/hyperframes), then inspect resting and mid-transition frames before sharing.

## Install

```text
/plugin install presentation-craft --marketplace victorarias/presentation-craft
```

On older Claude Code versions, add the marketplace first:

```text
/plugin marketplace add victorarias/presentation-craft
/plugin install presentation-craft@presentation-craft
```

To try it without installing, clone the repository and start Claude Code with
`claude --plugin-dir ./plugin`.

## What is included

- `plugin/skills/presentation-craft/SKILL.md`: three-stage workflow, shared storytelling and visual craft rules, style picker, and verification gate.
- `plugin/skills/presentation-craft/references/styles.md`: five selectable visual styles (**Contrast Reveal**, **Warm Editorial**, **Swiss Technical**, **Studio Dark**, and **Tactile Paper & Ink**) plus anti-slop rules.
- `plugin/skills/presentation-craft/references/live-html-deck.md` and `references/templates/live-deck-starter.html`: offline single-file 16:9 presentation architecture, presenter keyboard controls (`→`/`Space`, `←`, `1`–`9`/`0`, `Home`/`End`, `F`, `N`, `B`, `?`, `Esc`), URL hash state, `?still`/`?flat` fallbacks, and headless verification checklist.
- `plugin/skills/presentation-craft/references/hyperframes-video.md` and `references/templates/hyperframes-starter/`: multi-scene HyperFrames setup, intertitles and floating spotlight captions, box-clipped wipes, live DOM-measured canvas beams, FFmpeg music shaping, and an optional voiceover + SFX branch.

## Requirements

- **Live HTML decks**: any modern browser (zero runtime network dependencies).
- **HyperFrames videos**: Node.js 22+ and FFmpeg (`npx hyperframes`).

## Develop

Validate the plugin and marketplace manifests with Claude Code:

```sh
claude plugin validate ./plugin
claude plugin validate .
```

## License

MIT
