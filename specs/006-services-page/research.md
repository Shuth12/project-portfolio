# Phase 0 Research: Services Page

No `[NEEDS CLARIFICATION]` markers remained in the spec's Technical Context,
since this feature extends already-established static-site patterns (the
Contact page's pattern-background/off-white-card technique, the landing
page's hero heading style, and the Work gallery's project-subtitle/
project-body text styles). The items below record the small set of
implementation decisions made to keep the new page consistent with those
existing patterns, rather than open unknowns.

## Decision: Blob pattern background reuses the Contact page's tiled-background technique

- **Decision**: `Shelleycerny-blobs.png` is applied as a `background-image`
  on the page's full-bleed content area using the exact same properties as
  `.contact-pattern` (`background-repeat: no-repeat`, `background-position:
  center`, `background-size: cover`, `max-width: 75rem`, centered, `1.5rem`
  corner radius) — only the image URL differs from the Contact page.
- **Rationale**: The spec explicitly asks for the blobs pattern to be "the
  same size and look as" the Contact page's checkerboard pattern; the
  Contact page already solved exactly this (a single large decorative
  pattern image sized to fill a fixed-max-width rounded panel), so reusing
  the same CSS properties satisfies FR-003 with zero new layout mechanism.
- **Alternatives considered**: A tiled/repeating background (like
  `.wave-divider`'s repeating pattern) — rejected, since both the mockup and
  the source `Shelleycerny-blobs.png`/`Shelleycerny-checkared.png` assets are
  single large illustrations meant to be shown once at cover size, not
  repeated tiles.

## Decision: Off-white card with rounded corners and strong shadow reuses `.contact-card`'s shadow treatment, without the photo-overlap layout

- **Decision**: A new `.services-card` class reuses `.contact-card`'s
  background color, `1.5rem` border radius, and two-layer `box-shadow`
  (`0 2rem 3.5rem -1rem rgba(12, 11, 9, 0.6), 0 -0.75rem 2rem -0.75rem
  rgba(12, 11, 9, 0.5)`) for a "strong drop shadow," but without
  `.contact-card`'s flex/photo-overlap layout, since the Services card has
  no overlapping photo — it centers a heading and a grid instead.
- **Rationale**: Matches FR-004 ("rounded corners and a strong drop shadow")
  using an already-proven shadow value rather than inventing a new one,
  while keeping the card's internal layout (heading + grid, vertically
  stacked) simple and specific to this page's content.
- **Alternatives considered**: A single shared `.card` base class refactored
  out of `.contact-card` and `.services-card` — rejected as an
  out-of-scope refactor of working Contact-page CSS; duplicating the shadow
  value keeps this feature self-contained per the "don't add abstractions
  beyond what the task requires" guidance.

## Decision: "Services" heading reuses `.hero-card h1` styling

- **Decision**: The card's `<h1>Services</h1>` reuses the existing
  `.hero-card h1` rule (font-family, weight, color, size, letter-spacing,
  uppercase transform) via a page-specific selector (e.g. `.services-card
  h1`) with identical property values, rather than modifying the shared
  `.hero-card` rule itself.
- **Rationale**: Spec FR-005 requires the heading to be "styled consistently
  with the 'Hi I'm Shelley,' heading on the landing page"; matching the
  existing rule's property values (rather than sharing the selector, which
  is scoped to the hero section) keeps the landing page's markup/CSS
  untouched while achieving visual consistency.
- **Alternatives considered**: Renaming `.hero-card h1` to a shared class
  reused by both pages — rejected as broader-than-needed churn to existing,
  working CSS for a page that doesn't need it.

## Decision: Grid items reuse `.project-subtitle`/`.project-body` text styles in a new CSS Grid layout

- **Decision**: Each of the 6 service items is a small block with an
  `<img>` icon, an `<h2>` (or similar) subtitle reusing `.project-subtitle`'s
  font/size/color/letter-spacing values, and a `<p>` description reusing
  `.project-body`'s font/size/color values — but center-aligned (not the
  work-page's left/justified alignment) per FR-007. The six items sit in a
  new `.services-grid` using CSS Grid, 3 columns at desktop width,
  reflowing to fewer columns at narrower widths (FR-011).
- **Rationale**: Spec FR-007 explicitly calls for "subtitle (style of
  subtitles on work pages)" and "description in the body text style,"
  identifying `.project-subtitle`/`.project-body` (used on
  `work/*.html` detail pages) as the source styles to match, adjusted only
  for center alignment as shown in the mockup.
- **Alternatives considered**: Flexbox with `flex-wrap` instead of CSS
  Grid — workable, but CSS Grid's explicit column-count control makes the
  3-column desktop layout → fewer-columns-on-mobile reflow (FR-011) more
  direct to express and reason about for a fixed 6-item, evenly-sized grid.

## Decision: One new static HTML file, nav links updated in place

- **Decision**: `services.html` at the repository root, following the same
  file-naming convention as `index.html`/`work.html`/`contact.html`. The
  existing "Services" `<a href="#">` placeholder is updated to `<a
  href="services.html">` (or the relative `../services.html` from inside
  `work/`) on all 13 existing pages.
- **Rationale**: Matches constitution Principle I (no build step) and keeps
  the site's existing flat-file structure; this is the same pattern already
  used for the Work Gallery and Contact pages' nav-link rollouts.
- **Alternatives considered**: None — this is a direct continuation of the
  established site structure, not a new decision point.
