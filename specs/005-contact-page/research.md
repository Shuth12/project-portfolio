# Phase 0 Research: Contact Page

No `[NEEDS CLARIFICATION]` markers remained in the spec's Technical Context,
since this feature extends already-established static-site patterns (the
landing page's hero-card overlap technique, the Work gallery's off-white
card-on-color-panel treatment, and the constitution's existing "contact is a
`mailto:` link only" non-goal). The items below record the small set of
implementation decisions made to keep the new page consistent with those
existing patterns, rather than open unknowns.

## Decision: `mailto:` link styled as a button, no form, no JavaScript

- **Decision**: The "Send Me An Email" CTA is a plain
  `<a href="mailto:shelley.cerny@gmail.com">` styled with the existing
  `.button`/`.button--resume` classes — no `<form>`, no JS-driven mail
  composition, no third-party contact-form service.
- **Rationale**: The constitution's Explicit Non-Goals already rule out a
  contact form ("contact is a `mailto:` link only"); a plain anchor tag
  satisfies FR-009 with zero new dependencies and keeps the page usable with
  JavaScript disabled, consistent with Principle IV.
- **Alternatives considered**: A JS `mailto:`-on-click handler — rejected as
  unnecessary indirection when a plain `<a href="mailto:...">` already does
  this natively; a hosted form service (e.g. Formspree) — rejected, out of
  scope per the constitution's non-goals and would introduce a third-party
  network dependency.

## Decision: Checkerboard background as a tiled `background-image`

- **Decision**: `Shelleycerny-checkared.png` is applied as a repeating CSS
  `background-image` on the page's teal content area (the same element role
  as `.work-main`'s teal background), with `background-size` set so one tile
  repetition's width matches the off-white card's `max-width` (`75rem`,
  the same value already used by `.work-grid`/`.project-detail`), then
  tiled (`background-repeat: repeat`) to fill the full-bleed teal area
  behind the card, matching the mockup's edge-to-edge checkerboard.
- **Rationale**: The site already uses exactly this tiled-background-image
  technique for the header/hero `.wave-divider` (a repeating SVG data URI
  sized so one tile renders undistorted); reusing the same mechanism keeps
  the codebase consistent and requires no new CSS approach.
- **Alternatives considered**: Slicing the pattern into a single
  full-viewport-width raster image — rejected, wasteful (one small tile
  already repeats seamlessly) and not how the source asset was provided;
  an `<img>` element instead of a CSS background — rejected, since the
  pattern is decorative/non-content and CSS `background-image` is the more
  semantically correct choice (matches `.wave-divider`'s existing pattern).

## Decision: Card/photo overlap reuses the landing page's hero technique

- **Decision**: The off-white card and Shelley's photo overlap using the
  same `position: relative` + `box-shadow` + slight negative-margin overlap
  technique already established by `.hero-card`/`.hero-photo` on
  `index.html`, rather than a new layout mechanism.
- **Rationale**: `index.html` already solves "one element overlapping the
  corner of another, both with independent drop shadows" for the
  photo/pattern-backdrop/card cluster in the hero section; reusing that
  proven technique avoids introducing a second way to do the same thing.
- **Alternatives considered**: CSS Grid layering (`grid-template-areas`
  with overlapping cells) — workable but a heavier tool than the existing
  simple absolute/relative + negative-margin approach already in the
  codebase for this exact visual pattern.

## Decision: One new static HTML file, nav links updated in place

- **Decision**: `contact.html` at the repository root, following the same
  file-naming convention as `index.html`/`work.html`. The existing "Contact"
  `<a href="#">` placeholder is updated to `<a href="contact.html">` (or the
  relative `../contact.html` from inside `work/`) on all 12 existing pages.
- **Rationale**: Matches constitution Principle I (no build step) and
  keeps the site's existing flat-file structure; this is the same pattern
  already used for `work.html`'s nav link rollout in the Work Gallery Page
  feature.
- **Alternatives considered**: None — this is a direct continuation of the
  established site structure, not a new decision point.
