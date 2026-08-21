# Phase 0 Research: Work Gallery Page

No `[NEEDS CLARIFICATION]` markers remained in the spec's Technical Context,
since this feature extends an already-established static-site pattern
(landing page, `index.html` + `assets/css/styles.css`). The items below
record the small set of implementation decisions made to keep the new page
consistent with that existing pattern, rather than open unknowns.

## Decision: Grid layout mechanism

- **Decision**: Use CSS Grid (`display: grid`) for the Work gallery's
  thumbnail grid, with `grid-template-columns: repeat(5, 1fr)` on desktop,
  reflowing to fewer columns via `@media` breakpoints already established in
  `styles.css` (`64rem`, `48rem`).
- **Rationale**: The mockup shows a strict 5-column × 2-row grid of
  uniform-ish tiles — CSS Grid expresses this directly without extra
  markup, and the existing stylesheet already uses breakpoint-based
  reflow (see `.hero` at the `48rem` breakpoint) so the pattern is
  consistent with what's already in the codebase.
- **Alternatives considered**: Flexbox with `flex-wrap` — workable but
  needs more manual width math per breakpoint than Grid's `repeat()`;
  rejected in favor of Grid's simpler column control.

## Decision: One static HTML file per project detail page

- **Decision**: `work/<project-slug>.html`, one hand-authored file per
  project, no templating engine.
- **Rationale**: Matches constitution Principle I (no build step required)
  and Principle V (content changes confined to isolated files) — Shelley
  can add a new project by duplicating one existing detail page, swapping
  images/copy, and adding one grid entry, without needing developer help.
- **Alternatives considered**: A single `work.html` with in-page anchors
  per project (rejected — spec's User Story 2 explicitly asks for
  click-through to a distinct page per project, and the mockup's grid
  reads as a launch point, not an in-page index) — a JS-templated/data-
  driven page generated from a JSON manifest (rejected — would require a
  build step or client-side fetch, violating the static/no-build
  principle for zero real benefit at 10 projects).

## Decision: Project slugs and title casing

- **Decision**: Kebab-case URL slugs matching each display title:
  `the-yoga-space`, `red-cedar-coffee`, `bouncy`, `go-pint`,
  `boyd-consulting`, `invitations`, `fit4mom`, `book`,
  `wedding-signage`, `murals`.
- **Rationale**: Readable URLs, consistent with the existing `work.html`
  filename style already referenced by `index.html`'s nav link.
- **Alternatives considered**: Reusing the raw `assets/images/<folder>`
  names as slugs (e.g. `fit_for_mom`, `wedding_sign`) — rejected only for
  the page filenames/URLs (underscores read less cleanly in a URL); the
  underlying asset folder names are left untouched since renaming
  committed asset folders is out of scope and not requested.

## Decision: Thumbnail image reuse, no separate optimized copies

- **Decision**: The grid's `<img>` tags point directly at each project's
  existing `*_MockUp_Thumbnail.*` file; detail pages point directly at that
  project's other existing image files. No new image assets are generated,
  cropped, or resized as part of this feature.
- **Rationale**: All required imagery is already committed to the repo
  (confirmed during spec discovery); the PRD's "reasonably optimized"
  requirement is a pre-existing baseline for supplied assets, not a new
  processing step for this feature.
- **Alternatives considered**: Generating additional resized/`srcset`
  variants for responsive loading — rejected as unnecessary complexity for
  a ~10-image gallery at this scope; can be revisited later if page-weight
  becomes a measured problem.

## Decision: No JavaScript, no lightbox

- **Decision**: Both the grid and detail pages are pure HTML/CSS; images on
  detail pages are shown inline (e.g., a simple stacked/grid layout of
  `<img>` tags), not behind a JS lightbox/modal.
- **Rationale**: Constitution Principle IV allows JS only where CSS
  genuinely cannot provide the behavior; a full-page detail view served by
  a plain link satisfies User Story 2 without needing a lightbox.
- **Alternatives considered**: A JS lightbox/modal for viewing full-size
  images without leaving the grid — rejected; not requested by the user
  description or mockup, and against the "minimal JS" default.
