# Wood, Water & Waves — repo guide for Claude Code

A one-page promotional site about a wooden surfboard grown from a single Nantucket
tree and built by hand over one summer. Static HTML, no build step, deployed via
GitHub Pages.

Live: https://omniscopic.github.io/woodwaterwaves/

## Repo layout

```
index.html      the entire site — markup, all styling, all copy
support.js      runtime that renders index.html (do not edit)
image-slot.js   <image-slot> web component (do not edit)
uploads/        every photo and PDF thumbnail (~35 files)
```

Everything lives at the repo root. Pages serves the root of `main`; a push
redeploys automatically in about a minute.

## The one thing to understand first

`index.html` is not plain HTML. It is a **Design Component**: the page body sits
inside an `<x-dc>` element and is rendered at runtime by `support.js`. Practical
consequences:

- **All styling is inline `style="…"` attributes.** There are no CSS classes, no
  stylesheet, no design-token file. Repeat literal values. The only rules in
  `<helmet><style>` are `@font-face`/font links and body resets — leave that
  block alone.
- **`{{ name }}` holes are dotted lookups only** — never expressions. They are
  resolved by the `class Component extends DCLogic` script at the bottom of the
  file, in its `renderVals()` method. `{{ a + b }}` or `{{ fn() }}` fails
  silently; compute the value in `renderVals()` and expose it by name.
- **`<sc-if>` and `<sc-for>`** are the conditional and repeat elements. The three
  hero variants are wrapped in `<sc-if value="{{ heroCentered }}">` etc., driven
  by a `heroStyle` prop.
- **`<image-slot>`** is a drag-to-replace photo placeholder. Attributes:
  `id` (must be unique — the user's replacement is stored against it), `src`,
  `fit="cover|contain"`, `radius`, `placeholder`. A plain `<img>` is fine too
  when the image should show at natural proportions.
- `class` and `for` map to `className`/`htmlFor`; event handlers use JSX
  camelCase (`onClick="{{ handler }}"`).

Do not "clean this up" into a normal HTML file with a stylesheet. It would break
the authoring tool the owner uses upstream.

## Page order

Hero (3 switchable variants) · Intro · Where It Stands (current build status +
the three new-work photos) · As Told Elsewhere (4 press PDF cards + the YouTube
film) · Cedar log full-bleed · Poetic band · The Build (text) · Build photo
sequences · Frame by Frame gallery wall · Harbor full-bleed · Board detail trio +
lineup · In the Water strip · Project details · For Editors · Rich's bio · CTA ·
Footer.

Section boundaries are marked with `<!-- ====== NAME ====== -->` comments.

## Current framing (Aug 2026)

The project is no longer connected to **Banh Pho Surf Shop**, and Patrick
Broemmel is off the page — no shop name, address, map, or `banhpho.com` /
`instagram.com/banhphosurf` links. Rich builds alone in a small shack on
Nantucket; the location stays deliberately vague (no street address, no map
embed). The three community programs (Zen talks, yoga, community days) were cut
with the shop.

The board is **designed and framed** as of August 2026 and the build is
underway — `uploads/frames-cut.jpg`, `sunburst-wings.jpg`, `sunburst-fins.jpg`
are that evidence. Keep the status line in Project Details in step with reality.

The page's job is to introduce the project **and** foreground the press it has
already earned, to attract more of the same. That is why "As Told Elsewhere"
sits high, above the visual story, with outlet, byline, and year on every card.
`uploads/patrick_crop.png` is now unused but left in place.

## Design tokens (used as literals inline)

Colors
```
#F4E8D0  page background (sun-faded cream)
#EFE0C4  alternate light band
#3A2818  deep brown — dark bands, headings
#2A1D12  hero backdrop
#40301F  body text
#5C462E  secondary body text
#7A6144  captions
#C6592C  sunset orange
#A8431F  rust — eyebrow labels on light
#DA8A34  sun mid
#E7B84D  sun core
#D2982E  mustard
#6E7A31  avocado
#F7ECD2 / #F1DBB0 / #EFE0C0 / #EBC77A  creams on dark
```

Type
- Display / headings: **Yeseva One**, 400 only
- Body: **Bitter** (Georgia fallback); italic for pull quotes and captions
- Eyebrow labels: **Oswald**, uppercase, `letter-spacing: .34em–.42em`, 13–15px,
  always with matching `padding-left` so the tracking doesn't push it off-center

Motifs
- Radial-gradient sun disc: `radial-gradient(circle at 50% 45%, #E7B84D 0%, #DA8A34 50%, #C6592C 100%)`
- Striped divider: `repeating-linear-gradient(90deg, #C6592C 0 56px, #D2982E 56px 112px, #6E7A31 112px 168px, #3A2818 168px 224px)`
- Every photo carries `filter: sepia(0.2) saturate(0.94) contrast(1.03)`

Scale
- Fluid everywhere: `clamp(min, vw, max)` for font sizes and section padding
- Section padding pattern: `clamp(56px, 7vw, 96px)`
- Content widths: 760px (centered text), 900px (intro), 1280px (galleries)

Responsive
- One breakpoint: **720px**. Below it every multi-column grid collapses to a
  single column and photo heights shrink.
- There is no global `box-sizing` reset. Any full-width band written as
  `width: 100%` **plus** horizontal padding must carry `box-sizing: border-box`
  inline, or it overflows the viewport by twice the padding and its right edge
  gets clipped by the wrapper's `overflow-x: hidden` on phones.

## Adding a photo

1. Drop the file in `uploads/`. Filenames are **case-sensitive** on Pages —
   match them exactly.
2. Reference it as `uploads/Name.jpg`.
3. Use `<image-slot>` with a fresh unique `id` if it should stay swappable, or a
   plain `<img style="display:block; width:100%; height:auto; …">` for a
   full-width uncropped image.
4. Always include the sepia filter so it matches the rest.

## Deploying

```
git add -A && git commit -m "…" && git push
```
Pages rebuilds on push. If a change doesn't appear: check the **Actions** tab for
a queued or failed `pages-build-deployment` run, then hard-refresh.

## Conventions to keep

- No emoji. No new fonts. No new colors outside the list above — derive from it.
- Copy is warm and plainspoken, short sentences, no marketing hype.
- Credit lines: Rich Blundell (shaper), Patrick (photography).
