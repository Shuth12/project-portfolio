# Phase 0 Research: Landing Page (Home / About)

All Technical Context items were resolvable from the spec, the constitution,
and direct inspection of the reference mockup — no items needed to remain
as `NEEDS CLARIFICATION` going into Phase 1.

## Color palette

**Decision**: Use hex values sampled directly from
`assets/page_mockups/ShelleyCerny_WebsiteAbout.jpg` pixel data (via a
one-off Python/Pillow histogram of representative regions), rather than
estimating colors by eye.

| Role | Hex | Sampled from |
|---|---|---|
| Page background (cream/off-white) | `#F9F8F3` | Header and bio-card background regions |
| Hero panel background (teal) | `#1F7A8C` | Teal band behind the photo/bio panel |
| Accent shape (mustard yellow) | `#E8B601` | Yellow shape behind the photo; footer band |
| Heading / logo / nav text (green) | `#5D8C6A` | "HI I'M SHELLEY," heading and nav link glyphs |
| Body text (near-black) | `#0C0B09` | Bio paragraph text |
| CTA button background (purple) | `#9C8BBF` | "Download My Resume" button |
| Button / footer text (white) | `#FFFFFF` | Footer attribution and button label |

**Rationale**: Pixel sampling is materially more accurate than eyeballing a
palette, directly serving the constitution's Design Fidelity principle and
spec FR-006/SC-004 ("no unresolved visual deviations").

**Alternatives considered**: Manually eyeballing approximate hex values —
rejected as strictly worse given a repeatable sampling method was available
with no added tooling cost (Pillow is a one-off local dependency, not a
project dependency).

**Accessibility note** (feeds the spec's resolved contrast clarification):
computing WCAG contrast ratios against these sampled values confirms two
pairings fall below WCAG AA:

- Footer text (white `#FFFFFF`) on the mustard band (`#E8B601`): **~1.89:1** (AA requires 4.5:1 for normal text, 3:1 for large text — fails both).
- Nav text (green `#5D8C6A`) on the cream background (`#F9F8F3`): **~3.64:1** (fails AA's 4.5:1 for normal-size text; would pass the 3:1 large-text threshold).

Per the spec's clarification, both are shipped as-is (design fidelity wins);
this is documented in `plan.md`'s Complexity Tracking table as the
sanctioned constitution exception, not an oversight.

## Typography

**Decision**: Load two free Google Fonts via a CDN `<link>` tag (no
self-hosting, no build step):

- **Space Mono** (weight 700) for the nav links, the "HI I'M SHELLEY,"
  heading, and button/footer label text — pixel inspection of the mockup
  (`assets/page_mockups/ShelleyCerny_WebsiteAbout.jpg`) shows flat-terminal,
  evenly-spaced monospaced letterforms (e.g. the slab-like "S", uniform
  character widths in "HI I'M SHELLEY,"), not a rounded display face.
  Space Mono's bold weight closely matches that boxy, typewriter-like
  character. (Revised from an initial Baloo 2 pick, which read as too soft
  and rounded once compared side-by-side against the rendered page.)
- **Inter** (weight 400/500) for the bio paragraph body copy — a clean,
  highly legible sans that matches the mockup's plain body text without
  competing with the display font.

**Rationale**: No licensed font files were supplied (per the spec's
resolved clarification), so free equivalents are required. Both fonts are
open-license (SIL Open Font License), widely supported, and require no
build tooling — just a `<link>` in `<head>`, consistent with constitution
Principle I (no build step needed to publish).

**Alternatives considered**:
- Self-hosting font files in `assets/fonts/` — rejected for this feature:
  it adds binary assets and `@font-face` maintenance for a marginal
  offline/privacy benefit that isn't a stated requirement; revisit if a
  future spec needs it.
- System font stack only (no custom font) — rejected: the mockup's bold,
  monospaced display lettering is a distinctive part of the brand and a
  generic system sans would be a visible fidelity deviation.

## Decorative composition (scallop divider, layered photo accents)

**Decision**: Reproduce two structural decorative elements from the mockup
using CSS only (no images/SVG):

- A scalloped (wavy) divider between the header and the teal hero panel,
  built with a repeating `radial-gradient` background on a thin `<div>`.
  Pixel-sampling the mockup found a repeating bump pattern with a ~56px
  period and ~8px amplitude at the mockup's native resolution.
- A layered "stacked card" photo composition: the headshot sits above a
  same-sized mustard rounded-rect offset down-right (~17-18% of the
  photo's own size, derived by comparing the photo's and the mustard
  shape's edges in the mockup's pixel data), a thin cream vertical stripe
  overlaid near the photo's right edge, and a diagonally-striped
  cream/mustard block peeking out at the photo's bottom-left corner.

**Rationale**: These two elements are a significant part of the mockup's
visual identity (per constitution Principle II, Design Fidelity) but were
missed in the first implementation pass, which used flat/solid shapes
instead. Reproducing them with CSS shapes/gradients rather than image
assets keeps the page dependency-free and matches constitution Principle I.

**Alternatives considered**: Exporting the scallop/accent shapes as SVG or
PNG assets from the mockup — rejected for now since CSS reproduction is
close enough visually and avoids adding binary design assets to the repo;
revisit if a pixel-exact vector trace is later supplied by the designer.

## Logo and headshot assets

**Decision**: Reference placeholder paths (`assets/images/logo/...`,
`assets/images/profile/...`) in `index.html` without creating the actual
image files, mirroring the resume file's placeholder treatment (spec
FR-001, FR-002, FR-013). `alt` text on each `<img>` conveys the intended
content so the page degrades gracefully while the files are missing (spec
edge cases).

**Rationale**: Per the spec's clarifications, the real logo and headshot
files haven't been supplied yet; wiring up the correct relative paths now
means dropping the real files in later requires no HTML/CSS changes.

**Alternatives considered**: Checking in a temporary stock/dummy image —
rejected as unnecessary churn; the spec explicitly treats a missing/404
image as an acceptable, temporary state (same as the resume link).

## Mobile navigation

**Decision**: A pure-CSS responsive nav — flexbox with `flex-wrap`, no
JavaScript toggle/hamburger menu.

**Rationale**: Four nav items (About, Work, Contact, Services) plus a logo
comfortably wrap or stack at narrow widths without needing to hide content
behind a JS-driven menu. This satisfies constitution Principle IV, which
requires JavaScript only where CSS genuinely cannot provide the behavior —
here it can.

**Alternatives considered**: A JS-driven hamburger/off-canvas menu —
rejected as unnecessary for a 4-item nav and explicitly disfavored by the
constitution when a CSS-only approach works.

## Testing approach

**Decision**: Manual verification via `quickstart.md`, matching
`001-scaffold-site-deploy`'s precedent — no automated test framework.

**Rationale**: A single static content page with no interactive logic has
no meaningful unit/integration surface to automate; visual/manual
comparison against the mockup is the actual acceptance mechanism (spec
SC-004).

**Alternatives considered**: Visual regression tooling (e.g., a
screenshot-diff script) — rejected as disproportionate tooling for a
one-page static site with no build pipeline.
