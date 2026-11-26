# Live HTML deck reference

Use this reference when building a live, presenter-controlled browser presentation.

## Architecture: one self-contained offline HTML file

Deliver a single `index.html` that opens cleanly via `file://` or a tiny local static server with zero runtime network dependencies.
- **Zero external CDNs**: Inline all CSS, JavaScript, SVG icons, and small embedded images (base64 data URIs or local relative assets). A live talk must never depend on conference Wi-Fi.
- **Explicit color-scheme lock**: Set `<meta name="color-scheme" content="only light">` (or lock explicit background/text tokens) so browser dark-mode extensions or OS theme changes do not invert a pure-white opening into muddy grey.
- **Fixed 16:9 stage scaled cleanly to any screen**: Author layout in a fixed coordinate box (`1600x900` or `1920x1080`) and scale dynamically with `Math.min(window.innerWidth / W, window.innerHeight / H)` centered in a letterboxed viewport so diagrams never reflow or lose alignment on a projector.
- **Companion files beside `index.html`**:
  - `speaker-notes.md`: beat-by-beat spoken cues, timing targets, live-demo fallback instructions, and an "If asked" Q&A section.
  - `evidence.md` (when citing metrics or logs): maps every on-screen claim to its real source and transparently documents any fictionalized names, staged chat retellings, or compressed timestamps.

## Presenter controls and state

Every live deck must support these interactions:

| Input | Behavior |
| --- | --- |
| `ArrowRight` / `Space` | Next beat |
| `ArrowLeft` | Previous beat (snaps cleanly to its finished resting state without replaying entrance reveals backwards) |
| `1`–`9` / `0` | Jump directly to beat 1–9 / final beat |
| `Home` / `End` | Jump to opening / closing beat |
| `F` | Toggle fullscreen |
| `N` | Toggle speaker notes overlay (shows the current beat's notes) |
| `B` | Toggle blackout screen |
| `?` | Toggle keyboard shortcuts cheat sheet |
| `Escape` | Close notes, cheat sheet, or blackout |

**State and reliability guarantees:**
- **URL hash persistence**: Update `location.hash` (`#1`, `#2`, or `#beat-slug`) on navigation so reloading returns to the exact beat in its finished state.
- **Cancel in-flight timers on navigation**: Navigating forward or backward immediately cancels any pending typing, cursor, or `requestAnimationFrame` sequences so stray animations never bleed into another beat.
- **Reduced motion and 2D fallbacks**:
  - Support `?still` and `@media (prefers-reduced-motion: reduce)` to jump directly to resting states.
  - If the deck uses CSS 3D perspective (`perspective`, `transform-style: preserve-3d`), also support `?flat` for a clean 2D fallback.

## Choreography that feels cinematic and smooth

- **Split dramatic reveals across keypresses**: When an object appears and then flies across the stage to dock into a target, put the reveal on Beat N (holding cleanly at full readable size) and the flight + docking on Beat N+1. That puts timing in the speaker's hands instead of forcing awkward timed holds.
- **Make extraction and docking feel physical**:
  - When carving reusable pieces out of services, trace luminous seams around each boundary, gently lift the pieces, and leave dark recessed slots behind inside the original boxes so the viewer sees what stayed and what moved.
  - When docking a new piece into an existing system, measure the exact projected target slot via live `getBoundingClientRect()` (divided by stage `--scale`), animate the flight cleanly into the slot, flash both piece and container in a matching color on contact, and settle both into a new unified color before connecting downstream consumers.
- **Minimize crossing paths**: Order destination rows to mirror source positions so extracted cards glide directly into place rather than crossing over each other.
- **Keep transitions smooth at native display density**:
  - Separate 3D planes explicitly along `Z` (for example, floor at `-20px`, SVG connectors at `5px`, cards at `8px+`) so layers never z-fight or vanish on large high-DPI monitors.
  - Animate independent properties (for example, use CSS `scale` for an entrance pop so it never collides with a `transform` transition that moves the card on the next beat).
  - Avoid slapping `will-change: transform` onto every child node; excessive forced layer caching can cause boxes or SVG arrows to disappear in maximized Chrome windows.
- **Keep text legible through theme shifts**: When interpolating a canvas from pure white to deep obsidian (over `1.0–3.2s` for cinematic pacing), keep label opacity at `1` and compute or switch label ink from the surface luminance so contrast stays at or above `4.5:1` on every intermediate frame.
- **Authentic surfaces and crisp CLI moments**:
  - Recreate familiar workspaces (spreadsheets, chat threads, browsers) with genuine visual fidelity while replacing real colleagues' names with fictional ones so process lessons stay about systems, not individuals.
  - Stage terminal demos as a two-beat sequence: Beat A pulls back to show the diagram inside a browser on a desktop while a cursor clicks Terminal; Beat B zooms into the terminal, types the command, and shows real **colored** terminal output (clearly labeled `Recorded run` if not live).
  - When handing off to a colleague's demo, keep the shared architecture visible and give the next speaker's component a lively, unmistakable visual cue (such as an eager little shake and hop).

## Automated browser verification checklist

Verify the deck in headless Chromium / Playwright at standard viewports (`1600x900` and `1280x720`; avoid seizing the user's live fullscreen desktop):

1. **Offline load**: Open via `file://` or offline mode; confirm zero console errors, zero uncaught exceptions, and zero network requests.
2. **Every resting beat and mid-transition frame**: Capture screenshots of every beat plus intermediate frames during theme shifts, extractions, and docking flights. Check for clipped borders, dashed outlines touching text, missing boxes, or overlapping labels.
3. **Opacity-aware contrast check**: Sample real composited text/background contrast across light, transition, and dark frames; require `>= 4.5:1` everywhere.
4. **Navigation and rapid-advance checks**: Verify `ArrowRight`, `ArrowLeft`, direct hash links, reload persistence, `N`, `B`, `Escape`, `?still`, `?flat`, and advancing rapidly mid-animation (confirming timers cancel cleanly and card flights still interpolate).
