# Visual styles

Pick one aesthetic direction before designing any scene or slide, and commit to it completely. Offer the user 2 to 3 options suited to their topic (recommended choice first) so they choose the mood explicitly.

## Anti-slop commitments

Before applying any style, rule out default AI slide clichés:
- Never put an eyebrow + large title + subtitle + 3 identical icon cards + boxed bottom callout on the same frame.
- Never use generic purple-blue marketing gradients, floating glassmorphism blobs, or rainbow borders without semantic meaning.
- Reserve accent color for meaning (active state, passing check, error, or transformation beam), never decoration.
- Give the canvas generous breathing room: at least 30% open space on key beats.

---

## 1. Contrast Reveal (Obsidian & Light)

**Mood**: Dead-simple and familiar at the start, then a sudden, memorable plunge into a deep obsidian space with luminous precision accents and subtle depth.

**When to use**: Architecture evolutions, developer tooling launches, migrations from manual chaos to clean systems, or any story with a sharp before/after twist.

**Palette**
- Opening light act: canvas `#ffffff` or `#f8fafc`, primary ink `#0f172a`, muted `#64748b`, hairlines `#d5dce3`, friction callout `#b91c1c` on `#fef2f2`.
- Revealed dark act: canvas `#04080f` (or `#0b1115`), elevated card `#08101a`, borders `#243950`, primary ink `#eef4f9`, muted `#8da2b6`.
- Semantic accents (pick 1 primary + 1 secondary):
  - Cyan `#22d3ee` (data flow, declarative state, reads)
  - Emerald `#10b981` or `#22c55e` (verified pass, ready output, destination)
  - Coral `#f2867f` (caught errors, failed checks)
  - Warm amber `#f59e0b` (legacy/before state or warning)

**Typography**
- Display / intertitles: `Outfit` or `Space Grotesk` (`600`–`700`, tight tracking `-0.03em`, `76px`–`92px` on 1920x1080).
- Body / UI: `Inter` (`400`–`600`).
- Code / specs / counters: `JetBrains Mono` (`tabular-nums`).

**Signature techniques**
- Hold the opening act strictly light and flat (`0` glow, `0` 3D tilt) so the transition hits hard.
- Pivot via a deliberate physical transition: a horizontal scanline/laser sweep, a canvas darkening with glowing seams, or spreadsheet columns folding away into dark terminal space.
- Pair crisp DOM cards with an ambient background `<canvas>` drawing subtle radial glow, calm horizon gridlines, or `getBoundingClientRect()`-anchored photon beams.

---

## 2. Warm Editorial

**Mood**: Authoritative, calm, print-inspired journalism. High contrast without neon, built for following real numbers and evidence across views.

**When to use**: Operational walkthroughs, incident postmortems, observability/metrics tours, executive briefings, or data investigations.

**Palette**
- Light beat: warm newsprint `#f5f1e8`, deep charcoal ink `#181e20`, muted `#586163`, hairline `#c8cac0`, hard offset shadow `#cdddbd`.
- Dark beat (for contrast/tension): deep slate `#182022`, warm paper ink `#f5f1e8`, muted `#c0cdc9`, border `#344143`.
- Signal accents: sage green `#b6df8f` (healthy/reassuring), coral `#ff8777` (alert/anomaly), warm ochre `#e89037` (focus ring).

**Typography**
- Display headlines and big numerals: classic editorial serif (`Georgia`, `Newsreader`, or `Instrument Serif`, regular weight `400`, tight tracking `-0.05em`, `78px`–`104px`, `text-wrap: balance`).
- Body and narrative prose: clean grotesk (`Helvetica Neue`, `Inter`, or `DM Sans`).
- Data labels, timestamps, queue/metric names: crisp monospace (`JetBrains Mono` or `SF Mono`, `17px`–`20px`).

**Signature techniques**
- Alternate light and dark beats intentionally to mark shifts from "what looks fine" to "what is hidden underneath".
- Frame real screenshots or dashboard crops with sharp `1px` rules and offset solid shadows (`box-shadow: 15px 17px 0 #cdddbd`) instead of blurred drop shadows.
- Anchor big findings with an oversized serif numeral beside a single-sentence annotation and hairline top rule.
- Motion stays quiet and fast: subtle `translateY(14px)` rises (`0.45s ease-out`), never flashy beams or 3D tilt.

---

## 3. Swiss Technical / Blueprint

**Mood**: Razor-sharp engineering precision, architectural clarity, zero ornament.

**When to use**: Technical RFCs, performance benchmarks, protocol or API designs, compiler/pipeline architecture.

**Palette**
- Canvas: matte chalk `#f4f5f7` (or deep blueprint `#0d131f` if dark is preferred), card `#ffffff` with crisp `1px solid #d0d5dd`, primary ink `#111318`, secondary `#525866`.
- Single sharp signal accent: cobalt `#2563eb` OR vermilion `#dc2626` (never both as equals; keep the second strictly for errors).
- Subtle structural grid: `1px` lines at `4%`–`6%` opacity.

**Typography**
- Display & UI: geometric neo-grotesk (`Inter`, `IBM Plex Sans`, or `Plus Jakarta Sans`, crisp weight contrast `700` vs `400`, tight display tracking `-0.03em`).
- Numbers, tables, code: `IBM Plex Mono` or `JetBrains Mono` with `font-variant-numeric: tabular-nums`.

**Signature techniques**
- Strict asymmetric two-column grid (`1fr` diagram / `0.75fr` annotation) with visible hairline dividers.
- Linear clip-path wipes and ruler-like progress bars instead of soft fades.
- Use exact benchmark charts, callouts with leader lines, and before/after diffs rather than narrative illustrations.

---

## 4. Studio Dark

**Mood**: Clean, modern developer-tool showcase. Dark matte stage throughout so realistic UI replicas, terminals, and status transitions pop effortlessly.

**When to use**: Product demos, CLI/web app walkthroughs, feature launches where the live or reconstructed interface is the hero from frame one.

**Palette**
- Canvas: matte obsidian `#0e1014`, elevated surface `#181b21`, border `#2a2e36`, primary ink `#ffffff`, secondary `#b3b3b3`, muted `#6a7079`.
- Accents: one vivid hero accent (emerald `#10b981`, electric blue `#3b82f6`, or amber `#e3b341`), plus muted status tokens (amber waiting, violet build, crimson error, green live).

**Typography**
- Display & UI: `Inter` (`800` for hero headlines and kinetic stamps, `500`–`600` for labels).
- Terminal / identifiers: `JetBrains Mono` or `SF Mono`.

**Signature techniques**
- Kinetic horizontal timeline bars that physically stretch to convey wait time, paired with a ticking counter (`WEEK 1` -> `MONTH 4...`).
- Crisp, centered browser or app windows (`border-radius: 14px`, clean top chrome bar, highlighted URL) that keep the real interface front and center.
- Deliberate status flips (such as `TESTING` compressing out while `LIVE` expands with a clean ring pulse).

---

## 5. Tactile Paper & Ink

**Mood**: Warm, human, unhurried. Feels like an illustrated notebook or museum placard rather than software chrome.

**When to use**: Strategy narratives, design reviews, team rituals, customer stories, or talks to non-engineering stakeholders.

**Palette**
- Canvas: warm ivory `#fbf8f3`, secondary card `#f2ece1`, hairline `#dfd6c7`, ink `#1f1b18`, muted `#6c6258`.
- Accents: terracotta `#c85a32` (emphasis/friction), deep forest `#265c4b` (resolution/growth), muted gold `#b8892d` (highlight).

**Typography**
- Display: humanist serif (`Fraunces`, `Lora`, or `Georgia`, `500`–`600`, generous line-height `1.12`).
- Body: warm sans (`Source Sans 3`, `Plus Jakarta Sans`, or `Inter`).
- Annotations: `JetBrains Mono` at small uppercase tracking (`0.12em`).

**Signature techniques**
- Wide outer margins (`120px`–`160px`), generous line spacing, and clean SVG diagrams with `1.8px` rounded strokes.
- Slow, unhurried crossfades (`0.65s power2.out`) with minimal translation (`10px`–`14px`).
- Let one short sentence or one concrete quote own an entire frame before revealing supporting evidence.
