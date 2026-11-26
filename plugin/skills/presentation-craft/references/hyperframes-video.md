# HyperFrames video reference

Use this reference when rendering a self-playing 1920x1080 MP4 video from HTML compositions.

## Tooling: HyperFrames (public CLI)

[HyperFrames](https://www.npmjs.com/package/hyperframes) (`npx hyperframes`) is an open-source local HTML-to-MP4 renderer backed by headless Chrome and FFmpeg. Requirements: Node.js 22+ and FFmpeg.

```sh
npx hyperframes check                              # Lint, layout, runtime, and motion checks
npx hyperframes preview                            # Live browser preview with scrubbing
npx hyperframes render --output out/video.mp4      # Render 1920x1080 MP4 locally
```

Stay strictly local (`check`, `preview`, `render`). Never run remote/cloud publish commands unless the user explicitly asks to upload.

If the user is not using HyperFrames, the same composition, timing, GSAP timeline, and FFmpeg audio rules apply to any headless-browser HTML-to-video pipeline.

## Multi-scene composition layout

Split the video into clean scene files orchestrated by a root `index.html`:

```
video/
├── hyperframes.json
├── index.html                    # Root timeline sequencing all scenes
└── compositions/
    ├── scene-1-hook.html         # 10–12s: real starting state -> slow feedback loop -> pivot sweep
    ├── scene-2-mechanism.html    # 10–12s: dedicated beat for the core architectural shift
    ├── scene-3-walkthrough.html  # 20–30s: calm spotlight code or working-prototype UI tour
    ├── scene-4-proof.html        #  9–11s: real validator / metrics / parity proof
    └── scene-5-close.html        #  7–8s:  horizon visual + title + single link
```

**Root contract (`index.html`)**
- Fixed viewport: `1920x1080`, `fps: 30`, `overflow: hidden`.
- Each scene mounts via a `.scene-host` `<div>` with `data-composition-id`, `data-composition-src`, `data-start`, `data-duration`, `data-track-index="1"`, `data-track-kind="graphics"`, `data-width="1920"`, `data-height="1080"`.
- Root script creates a paused GSAP timeline spanning total duration (`tl.to({}, { duration: TOTAL }, 0); window.__timelines["main"] = tl; tl.seek(0);`).

**Scene contract (`compositions/scene-*.html`)**
- Wrap each scene in `<template>` with scoped `<style>`, `#root` (`data-composition-id`, `data-width="1920"`, `data-height="1080"`), and `<script>` registering `window.__timelines["scene-id"] = tl; tl.seek(0);`.
- Mark decorative canvases, backdrops, scanlines, and transition overlays with `data-layout-ignore="true"` so `hyperframes check` does not report false overlap warnings.
- Initialize hidden elements deterministically at `t=0` (`tl.set(..., { opacity: 0 }, 0)`) and drive all `<canvas>` draws from a GSAP clock tween (`tl.to(clock, { t: DUR, duration: DUR, ease: "none" }, 0)` with `onUpdate: () => draw(clock.t)`) so arbitrary frame seeking renders identically every time.

## Pacing and visual-first storytelling (default)

When there is no voiceover, text and visuals share the storytelling job cleanly:

| Beat type | Duration | Staging rule |
| --- | --- | --- |
| Full-screen typographic intertitle | `1.8–2.2s` | Centered on an empty canvas, 1 short sentence (max 8–10 words), silky `expo.out` entrance (`0.7s`), fade out before the stage enters |
| Opening state + friction | `10–12s` | Start with the real current foundation (e.g. a published spec or existing workflow), show why mistakes stay easy and feedback is slow, then sweep into the revealed world (`~0.9s`) |
| Core shift (dedicated scene) | `10–12s` | Give the breakthrough its own dedicated moment (e.g. transforming imperative logic into declarative rules in place, then fanning out to multiple consumers) + one quiet unboxed summary line |
| Spotlight code or prototype tour | `20–30s` | Hold the main editor or realistic browser window steady; allocate `5.5–7.0s` per sub-beat with one quiet floating spotlight caption (`01 Verb phrase` + muted secondary clause). When showing a working prototype, highlight the actual live URL clearly in the browser address bar and animate concrete end-to-end flows inside it |
| Visual transformation / Prism | `10–12s` | Stage concrete input artifacts streaming into a central engine and emerging as validated output, anchored by a crisp **single-line** equation (`white-space: nowrap`) |
| Proof / verification scene | `9–11s` | Real CLI or validator output + animated parity/progress grid + 3 hairline typographic pillars (light and airy, never heavy cards) |
| Closing horizon | `7–8s` | Title + one calm horizon line + single URL or repo path; keep subtle ambient motion alive through the audio fade-out |

Total target length: **65 to 80 seconds** for a focused single-topic launch video; **100 to 120 seconds** for a unified two-part story.

## Motion and geometry craftsmanship

- **Calm, polished glides**: Use `expo.out` (`0.65–0.85s`) for major panels and intertitles, `power3.out` (`0.45–0.65s`) for staggered items, and `power2.inOut` (`0.4–0.5s`) for fades and wipes. Keep box motion smooth and restrained rather than jumpy or bouncy; reserve `back.out` stamps strictly for rare celebratory moments (such as a `LIVE` pill burst).
- **Pixel-exact canvas beams**: Measure live DOM element edges inside `draw(t)` relative to `#root` so bezier curves and travelling light pulses always touch real card borders cleanly:
  ```js
  function rectOf(id, rr) {
    const el = document.getElementById(id);
    if (!el) return null;
    const r = el.getBoundingClientRect();
    if (r.width <= 0 || r.height <= 0) return null;
    return {
      left: r.left - rr.left,
      right: r.right - rr.left,
      cx: (r.left + r.right) / 2 - rr.left,
      cy: (r.top + r.bottom) / 2 - rr.top,
    };
  }
  ```
- **Box-clipped code/state wipes**: Transform card A into card B cleanly inside its rounded border with zero overflow or ghosting:
  1. Stack two opaque panels (`position: absolute; inset: 0;`) inside a container with matching `border-radius` and `overflow: hidden`.
  2. Animate panel A's `clipPath` from `inset(0 0 0 0%)` to `inset(0 0 0 100%)` while simultaneously animating panel B's `clipPath` from `inset(0 100% 0 0)` to `inset(0 0% 0 0)`.
  3. Glide a narrow glowing scan beam (`#scan-beam`, `data-layout-ignore="true"`) across `x` in lockstep (`power2.inOut`), confined strictly inside the card bounds.
- **Single-line visual lockups**: Size key equations (`Unstructured input -> Ready to ship`) with `white-space: nowrap` and visual framing so they read as an intentional graphic lockup, never wrapped body copy.
- **No competing headers or boxed subtitles**: Leave slide titles, eyebrows, and explanatory card subtext off the stage. Let intertitles and floating spotlight captions tell the story cleanly.

## Audio design: shaped music bed (default)

Shape one royalty-free instrumental track (or clean ambient loop) to mirror the visual arc using FFmpeg:

1. **Opening contrast (for Contrast Reveal)**: Apply a gentle low-pass filter (`lowpass=f=650`) and slightly lower gain during the light opening beats, then crossfade cleanly to full spectrum at the exact timestamp of the visual pivot transition (e.g. `t = 11.0s`).
2. **Ending fade**: Fade out smoothly over the final `4.0–5.0s` (`afade=t=out:st=END_MINUS_4.5:d=4.5`).
3. **Target levels**: Mix to roughly `-16` to `-18 dB` mean volume with a soft limiter (`alimiter=limit=0.95:level=false`) so peak stays safely below `-0.2 dB`.

Example FFmpeg music shaping + mux:

```sh
PIVOT=11.0
TOTAL=75.5
FADE_START=71.0

ffmpeg -y -i rendered-visual.mp4 -stream_loop -1 -i music.wav \
  -filter_complex "\
    [1:a]atrim=0:$TOTAL,afade=t=in:d=1.2,afade=t=out:st=$FADE_START:d=4.5,asplit=2[m1][m2];\
    [m1]lowpass=f=650,volume=0.22,atrim=0:$PIVOT,afade=t=out:st=$(echo "$PIVOT - 0.6" | bc):d=0.6[intro];\
    [m2]volume=0.35,atrim=start=$(echo "$PIVOT - 0.6" | bc):end=$TOTAL,asetpts=PTS-STARTPTS,afade=t=in:d=0.6,adelay=$(echo "($PIVOT - 0.6) * 1000 / 1" | bc)|$(echo "($PIVOT - 0.6) * 1000 / 1" | bc)[main];\
    [intro][main]amix=inputs=2:duration=longest:normalize=0,alimiter=limit=0.95:level=false[aout]" \
  -map 0:v -map "[aout]" -c:v copy -c:a aac -b:a 192k -shortest final-video.mp4
```

## Optional branch: voiceover + synced SFX

Use this branch only when the user asks for spoken narration (for example, an all-hands walkthrough of a multi-step UI flow):

- **Calm engineer register**: Plain declaratives, varied sentence lengths, understatement, one real punch reserved for the key finding. Skip staccato fragment pairs, rhetorical questions, and "Not anymore" pivots.
- **Time scenes to measured VO duration**: Record or generate narration per scene first, measure each clip with `ffprobe`, add `0.3–0.4s` lead-in and `0.5–0.8s` breathing tail, and size each scene to match.
- **Layer audio cleanly**: Spoken VO in foreground (`~ -16` to `-18 dB`), subtle instrumental bed underneath (`volume=0.05`–`0.08`), and sparse one-shot UI SFX (`click`, `pop`, `chime`, `thud`) placed at exact visual action timestamps.
- **Verify zero accidental dead air**: Run `ffmpeg -i final.mp4 -af "silencedetect=n=-50dB:d=1.5" -f null -` (intentional pauses on celebratory beats are fine).

## Pre-delivery QA checklist

1. Run `npx hyperframes check` and resolve every lint, runtime, layout, and motion warning (`ok: true`, `0` warnings).
2. Render the MP4 and extract keyframes at **mid-transition moments** (mid-wipe, mid-beam, each spotlight step, browser URL bar, final lockup) as well as resting frames. Visually inspect every frame for overflow, alignment drift, ghosting, or awkward line wraps.
3. Verify audio levels (`volumedetect`) and absence of clipping or unintended silence.
4. Confirm zero internal hosts, private data, or unverified numbers appear anywhere in any frame.
