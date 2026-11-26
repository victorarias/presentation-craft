---
name: presentation-craft
description: Design and build striking technical presentations, live interactive browser decks, and HTML-to-MP4 explainer or launch videos. Use whenever the user asks to create a presentation, slide deck, demo deck, talk visuals, launch video, product walkthrough video, visual explainer, or HyperFrames composition, even if they only mention "making slides", "a demo video", or "explaining a project visually".
---

# Presentation craft

Build presentations and explainer videos that feel authored, memorable, and alive. One shared storytelling and visual craft powers two delivery formats:

- **Live HTML deck**: a single self-contained, offline-ready, keyboard-driven 16:9 browser presentation for live talks and demos.
- **HyperFrames video**: a deterministic 1920x1080 MP4 video rendered locally from HTML, CSS, GSAP, and Canvas via `npx hyperframes`.

## 1. Work in three stages (never skip straight to building)

Great presentations come from getting the story and visual hook right before writing HTML. Read existing project files first so you only ask what the user must decide.

### Stage 1: Agree the story
Align on five essentials before proposing visuals:
1. **Format and budget**: Live HTML deck (`3–5 min`), HyperFrames MP4 video (`60–120s`), or both from one shared story.
2. **Audience and one takeaway**: What they already know (skip intro boilerplate they know) and the single shift in thinking you want by the end.
3. **The four pillars** (in whatever order serves the tension): why this mattered, what you built, the real value it unlocks, and how someone uses it.
4. **Honest starting state**: Ground the opening in what exists today rather than a strawman before-state. Calibrate claims carefully ("some users", "could use this approach") and gather real code, CLI transcripts, UI screens, or data rows.
5. **Audio mode (video only)**: Default to **visual-first with a shaped music bed** (intertitles + floating spotlight captions carry the story). Offer **voiceover + SFX** as an explicit alternative when spoken narration is essential.

### Stage 2: Design how to tell it and make it visually interesting
Before coding, propose the visual concept and get agreement:
1. **Pick one visual style**: Offer 2 to 3 fitting directions from [references/styles.md](references/styles.md) (recommended default first) and commit fully to that single palette, typography, and motion mood.
2. **Invent one or two novel visual moments**: HTML and Canvas break free of static slide templates. Propose concrete spatial metaphors tailored to the story:
   - Transforming a familiar artifact in place (a faithful spreadsheet folding away columns until only glowing commands remain; imperative code wiping into declarative rules inside the same card).
   - Revealing hidden structure (carving luminous modules out of a flat diagram and lifting them into a shared layer while leaving recessed slots behind; docking a new puzzle piece into a library slot so both flash and settle into a unified color).
   - Pulling the camera into the real workspace (zooming out to reveal the diagram sits inside a browser window on a desktop, animating a cursor clicking Terminal, then zooming into live colored CLI output; showing a working prototype inside a realistic browser with the live URL highlighted in the address bar).
   - Turning an abstract transformation into a physical visual (multiple messy inputs streaming into a luminous Prism and emerging as clean output, paired with a crisp single-line lockup).
3. **Plan small human beats**: A brief moment of personality, such as a candid chat message followed by an honest failure the next day, or an eager handoff card gently vibrating for the next speaker's demo, makes technical talks memorable.

### Stage 3: Build, verify visually, and polish with the user
Only after Stages 1 and 2 are aligned, build the deck or video, inspect rendered frames (especially mid-transition), and iterate on pacing and feel.

## 2. What makes a presentation look genuinely good

Apply these positive craft principles across every style and format.

### Lead with tension, transform one persistent world
- **Open cleanly**: Start with one crisp question (plus a quiet muted subtitle if needed) or a familiar real-world artifact. Let the opening breathe with zero extra diagrams or chrome.
- **Keep one continuous stage**: Mutate what is already on screen so the viewer tracks causality effortlessly. When returning to a system later in the story (for example, showing a real failure), bring back the real architecture diagram rather than shrinking it to a generic box.
- **Reflect real causality in layout**: Position entry/routing nodes at the top, helper services alongside, and downstream components below. Align animation destinations cleanly with their origins so moving pieces travel short, direct paths without tangling.

### Let visuals breathe with clear text hierarchy
- **Remove competing chrome**: Put a title on the opening frame only. Drop recurring slide headers, eyebrows, card subtext (if a card says `Schema Rules` and `61`, cut the paragraph below it), decorative "up next" footers, and generic labels.
- **Stage story text deliberately (visual-first videos)**: Blend two clean devices so story copy owns its own visual tier:
  1. **Full-screen typographic intertitles** (`1.8–2.2s`): one short sentence centered on an empty canvas before the diagram enters.
  2. **Quiet floating spotlight captions**: one unboxed line (`01 Describe the input` + muted secondary clause) above the stage.
- **Keep key equations on one crisp line**: Size headline lockups (`Unstructured input -> Validated output`) with `white-space: nowrap` so they never break awkwardly across two lines.

### Show authentic artifacts, paced for reading
- **Faithful surfaces**: When showing a spreadsheet, chat thread, spec page, browser, or terminal, build it to look genuinely like the real tool (with colored terminal output and visible URL bars), while anonymizing real people's names and private customer data.
- **Unhurried code and UI spotlights**: Bring a code editor or browser window in once and keep it rock-steady across 3 to 4 beats (`5.5–7.0s` each). Light up only the active block with a subtle tint and left accent border while dimming inactive blocks (`opacity: 0.3`), paired side-by-side with its live result (autocomplete, plain-English error, preview card, packaged output).
- **Earn credibility with honest proof**: Include a real caught error, a genuine limitation, or a real production failure that improved the system. Clearly distinguish illustrative retellings or compressed timestamps from recorded evidence in companion notes.

### Craft cinematic, exact motion
- **Cinematic pacing and smooth glides**: Give major visual shifts unhurried timing (`1.0–3.2s` for world dark-shifts or extractions). Use smooth `expo.out` / `power3.out` glides (`0.55–0.85s`) for entrances and `power2.inOut` (`0.4–0.5s`) for exits, keeping abrupt opacity flashes and bouncy overshoot off layout cards (reserve punchy overshoot strictly for rare celebratory stamps like a `LIVE` status flip).
- **Give presenter control over dramatic beats (live decks)**: When a beat has a reveal followed by a transformation or docking flight, split them onto consecutive keypresses instead of trapping the speaker in a long timed hold.
- **Pixel-exact geometry**: Anchor canvas beams, connectors, and docking flights to live `getBoundingClientRect()` coordinates. Clip scanline wipes cleanly inside rounded card borders using `overflow: hidden` and inverse `clip-path: inset(...)` on opaque stacked panels.
- **Full-contrast transitions**: During light-to-dark shifts, switch text ink directly from background luminance so labels stay crisp (`>= 4.5:1`) on every intermediate frame instead of washing out through pale grey.

## 3. Choose a visual style

Load [references/styles.md](references/styles.md) in Stage 2. Present the best-fitting options and commit fully to one style's palette, typography, lighting, and motion mood:

| Style | Visual arc & mood | Best for |
| --- | --- | --- |
| **Contrast Reveal** | Crisp light mundane opening dropping into deep obsidian with luminous accents and subtle depth | Architecture shifts, technical breakthroughs, launch demos with a before/after twist |
| **Warm Editorial** | Warm newsprint paper alternating with deep charcoal slate, display serif + monospace data annotations | Operational walks, postmortems, metric investigations, executive briefings |
| **Swiss Technical** | Matte chalk canvas, deep ink, hairline grids, tabular numerals, one sharp signal accent | Engineering RFCs, benchmarks, systems design |
| **Studio Dark** | Deep matte dark canvas throughout, restrained elevation cards, one vivid accent, crisp UI replicas | Product walkthroughs and feature demos where the app UI is the star |
| **Tactile Paper & Ink** | Warm ivory, espresso ink, terracotta and forest accents, generous whitespace | Strategy stories, design reviews, human-centered narratives |

## 4. Build by delivery format

After aligning on story, visual concept, and style, load the format reference you need:

- **Live interactive HTML presentation**: read [references/live-html-deck.md](references/live-html-deck.md) and start from [references/templates/live-deck-starter.html](references/templates/live-deck-starter.html).
- **HyperFrames MP4 video**: read [references/hyperframes-video.md](references/hyperframes-video.md) and start from [references/templates/hyperframes-starter/index.html](references/templates/hyperframes-starter/index.html).

## 5. Verification gate before sharing

Check the real rendered output before presenting it:

1. **Inspect mid-transition frames**, not just resting states. Catch clipped borders, misaligned beams, overlapping outlines, ghosting panels, or low-contrast transitions before the user sees them.
2. **Verify readability and contrast**: Confirm every visible foreground/background pair stays at or above `4.5:1` across resting and transition frames.
3. **Check factual and privacy boundaries**: Confirm every number matches real evidence, real names are anonymized where needed, and zero private hosts, secrets, or customer records appear on screen.
4. **Run format-specific checks**:
   - Live HTML deck: offline file load, forward/back/reload navigation, timer cancellation on rapid advance, `?still` and `prefers-reduced-motion`, 16:9 scaling at headless `1280x720` and `1600x900` (avoid commandeering the user's live fullscreen display).
   - HyperFrames video: `npx hyperframes check` (`ok: true`, zero warnings), keyframe inspection across every scene and mid-transition, and audio checks (mean `-16` to `-18 dB`, peak below `-0.2 dB`, clean fade-out, zero unintended dead air).
5. **Refine on feel with the user**: Share a preview or local URL, ask what feels too fast, too cluttered, or misaligned, and tighten before final delivery.
