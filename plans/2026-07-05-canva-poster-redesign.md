# Plan: Rebuild landing page from poster design (v2 — minimal light design)

Source of truth: `what is rap.pdf` page 2 (page 1 is the obsolete chalkboard
design). Mock reference: `WhatsApp Image 2026-07-05 at 16.47.44.jpeg`.

Design: light warm-grey background · handwritten "what is rap?" title ·
centered polaroid ("mit rap club") · two event blocks, each a mono date over
an italic sans label in a grey box. Hackathon (7.18–7.19) left, salon/cypher
(7.17) right.

**Estimated fidelity: ~100%** — fonts, colors, and layout metrics are now
extracted from the PDF itself; the title is pixel-exact extracted artwork.

## Confirmed from the PDF (2026-07-05)

**Fonts (actual, embedded):**
- Title: **Six Hands Chalk** (commercial Canva font — do NOT license/embed;
  we use extracted artwork instead, see assets)
- Dates: **Anonymous Pro Bold** — free on Google Fonts, exact match
- Labels: **Arial Italic** (18pt in PDF) — system font, use
  `font: italic 1.x Arial, Helvetica, sans-serif`

**Colors (sampled from PDF render):**
- Page background: `#dfddd6`
- Label box grey: `#c3c3c0`
- Ink / text: `#1b1a19` (labels render pure black)

**Layout metrics (PDF points, 612×792 page), for proportions:**
- Title bbox: x 176–421, y 105–204 (≈40% page width, centered)
- Polaroid visible area: x ≈169–443, y ≈207–508
- Dates at y≈575 (14.7pt / 13.5pt); labels at y≈598–618
- Event columns centered around x≈186 (hackathon) and x≈424 (salon/cypher)

**Assets (done, in `assets/`):**
- `assets/title-what-is-rap.png` — 1384×322 transparent PNG, exact Six Hands
  Chalk artwork extracted at 400dpi from the PDF (avoids font licensing;
  displayed ≤ ~460px wide so 3x retina headroom)
- `assets/polaroid.png` — 435×490, cropped from the 840×840 embedded photo to
  match the poster's clip exactly. Max resolution the source photo allows
  (~1.1x at display size); ask the friend for the original photo if sharper
  is wanted.

**Bonus info found in the full embedded photo** (the poster crops it out;
available if the user wants it on the site): salon 4–8pm July 17 · hackathon
full day July 18–19 · location MIT Media Lab [e15-341] · names: Elan
Barenholtz, Michael Levin, Nick Montfort, Wasalu [Lupe Fiasco] Jaco.

## Build steps

1. ~~Get assets~~ Done (extracted from PDF).
2. Rewrite `index.html`: light theme (`#dfddd6`), single centered column —
   title image (with real `<h1>` text visually-hidden for SEO/a11y) →
   polaroid → two event links side by side (stack on narrow screens).
3. Load Anonymous Pro Bold from Google Fonts; Arial Italic via system stack.
   Drop Fredoka/Young Serif/Space Mono.
4. Strip all CRT machinery: animations, SVG warp filter, static overlays,
   `?power=` flag, ring logo, `assets/noise.png` + `assets/voxel.png` if unused.
5. Update `theme-color` (`#dfddd6`) and favicon to match the new palette;
   keep lu.ma links on the event blocks.

## Decisions

- **CRT design (2026-07-05):** replaced entirely, no feature flag — git
  history holds the old version.
- **Title font:** use extracted PNG artwork, not a lookalike font (exact match,
  no license issues). Fallback text stays in the DOM for accessibility.

## Open questions

- Event order: mock lists hackathon before salon/cypher. Default: match the mock.
- Motion: design reads intentionally still. Default: none beyond link hover states.
- Add the time/location/speaker details found in the photo, or keep the page minimal?
