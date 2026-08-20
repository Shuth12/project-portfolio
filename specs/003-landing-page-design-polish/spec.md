# Feature Specification: Landing Page Design Polish

**Feature Branch**: `003-landing-page-design-polish`

**Created**: 2026-08-19

**Status**: Draft

**Input**: User description: "I have a few notes from the designer on the landing page before we move on. 1. for the picture with the underlay lets show a little more of the underlay. 2. more padding on the main content the images and the main text box additionally make the text block take up less space (more square), add more padding between the text and the image underlay 3. do not use m dashes anywhere on the site and more letter spacing 4. also lets bump the letter spacing in the nav bar a lot more, nothing drastic."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Hero visual shows more of the patterned underlay (Priority: P1)

A visitor lands on the homepage and sees the designer's signature patterned
backdrop peeking out more prominently from behind Shelley's photo, so the
layered, hand-crafted feel the designer intended actually reads at a glance
instead of being mostly hidden behind the photo.

**Why this priority**: This is a specific, easily-verified visual correction
the designer flagged first and is purely visual (no layout risk to other
elements), making it the safest and fastest to validate.

**Independent Test**: Load the homepage and visually compare the exposed
margin of the patterned backdrop around the photo against the current
(pre-change) version — a clearly larger sliver of pattern must be visible on
the offset edges, with the photo and backdrop still cleanly aligned.

**Acceptance Scenarios**:

1. **Given** the homepage hero section, **When** it renders on desktop,
   **Then** the patterned backdrop behind the profile photo is visibly
   revealed by a noticeably wider margin than before on the offset side(s),
   while the photo remains fully intact and undistorted on top of it.
2. **Given** the homepage hero section, **When** it renders at tablet and
   mobile breakpoints, **Then** the increased backdrop reveal scales
   proportionally and does not cause the backdrop to spill outside the hero
   visual's bounding area or get clipped awkwardly.

---

### User Story 2 - Main content, image, and text block get more breathing room (Priority: P1)

A visitor sees a homepage where the overall content area, the hero image,
and the bio text block all have generous surrounding space, and the bio text
block itself reads as a more compact, squared-off panel rather than a wide,
short strip, with a clear gap between the text block and the image/underlay
behind it instead of the two crowding each other.

**Why this priority**: This is the designer's core layout-balance note and
affects the primary above-the-fold impression of the site, so it carries
equal weight to the underlay fix and should ship in the same pass.

**Independent Test**: Load the homepage and confirm, without any other
changes, that (a) the outer content padding around the hero section has
visibly increased, (b) the bio text card's proportions are closer to square
(reduced width relative to height compared to the current version) with
increased internal padding, and (c) there is clearly more visual separation
between the text card and the image/backdrop behind it.

**Acceptance Scenarios**:

1. **Given** the homepage main content region, **When** it renders on
   desktop, **Then** the padding surrounding the hero section (between the
   content and the page edges/header) is visibly larger than before.
2. **Given** the bio text block, **When** compared to its current width and
   height proportions, **Then** it occupies a narrower, more square-shaped
   footprint rather than an elongated wide strip, and its internal padding
   (space between its border and its text/button content) is visibly
   increased.
3. **Given** the bio text block and the image/underlay behind it, **When**
   viewed together, **Then** there is visibly more separation/space between
   them than in the current layout, without breaking the intentional
   overlap accent between the two elements.
4. **Given** the updated hero layout, **When** viewed at tablet and mobile
   breakpoints, **Then** the increased padding and squared text block remain
   legible and do not cause overlapping content, horizontal scrolling, or
   awkward cramping.

---

### User Story 3 - No em dashes and increased letter spacing sitewide (Priority: P2)

A visitor reading any text on the site (page titles, headings, body copy)
never encounters an em dash character, and notices the text has a slightly
more open, deliberate letter spacing consistent with the site's
typographic style.

**Why this priority**: This is a sitewide copy/typography consistency pass
rather than a structural layout change, so it can land right after the
layout fixes without blocking them.

**Independent Test**: Search all visible site text (including the page
title and meta description) for the em dash character and confirm none
remain; separately, compare body text letter spacing against the current
value and confirm it has increased.

**Acceptance Scenarios**:

1. **Given** any page of the site, **When** its visible text and HTML
   `<title>`/meta content are inspected, **Then** no em dash character
   appears anywhere; sentences that previously used an em dash read
   naturally with alternative punctuation (e.g., comma, period, or
   restructured phrasing) instead.
2. **Given** the site's body/paragraph text, **When** compared to its
   current letter spacing, **Then** the spacing is modestly increased in a
   way that remains easily readable and consistent across the page.

---

### User Story 4 - Navigation bar letter spacing increased (Priority: P3)

A visitor scanning the navigation bar sees the nav link labels with
noticeably more open letter spacing than before, giving the nav a more
deliberate, editorial feel without looking stretched or broken.

**Why this priority**: This is a narrowly-scoped, low-risk tweak isolated to
the nav bar and is the most cosmetic of the four notes, so it can be
validated last.

**Independent Test**: Load the homepage and compare the nav link
letter-spacing value against the current baseline (0.08em) — it must be
clearly larger while nav items still fit on one line at each supported
breakpoint without wrapping or overlapping the logo.

**Acceptance Scenarios**:

1. **Given** the site header navigation, **When** it renders on desktop,
   **Then** the nav link letter spacing is noticeably wider than the
   current baseline while still reading as a subtle, intentional
   adjustment rather than an extreme stretch.
2. **Given** the site header navigation, **When** it renders at the
   mobile breakpoint where the nav stacks/centers, **Then** the increased
   letter spacing does not cause nav items to wrap onto multiple lines or
   overflow their container.

### Edge Cases

- What happens to the hero layout's corner-overlap accent between the photo,
  backdrop, and text card once both the backdrop reveal and the text/image
  spacing increase — do the two adjustments conflict, and if so, which
  takes precedence? (See Assumptions.)
- How does the more-square text block interact with the existing hero grid
  column ratio at the tablet breakpoint, where space is already narrower?
- Does increasing nav or body letter spacing at the narrowest mobile
  breakpoint cause any text to wrap or truncate where it didn't before?
- Are there other pages or components beyond the current homepage (e.g. a
  future Work page) that also need the no-em-dash and letter-spacing rules
  applied once they exist?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The homepage hero visual MUST reveal a noticeably larger
  margin of the patterned backdrop around the profile photo than the
  current design, while keeping the photo and backdrop cleanly aligned and
  undistorted.
- **FR-002**: The homepage main content area MUST use increased outer
  padding compared to its current value, applied consistently across
  desktop and responsive breakpoints.
- **FR-003**: The hero bio text block MUST use increased internal padding
  compared to its current value.
- **FR-004**: The hero bio text block's proportions MUST be adjusted to
  read as more square (reduced width relative to its height) than the
  current wide, short layout.
- **FR-005**: The spacing between the hero bio text block and the hero
  image/backdrop MUST be visibly increased compared to the current layout.
- **FR-006**: No em dash character MUST appear anywhere in the site's
  markup-rendered text or metadata (titles, meta descriptions, headings,
  body copy); existing em dashes MUST be replaced with alternative
  punctuation or phrasing that preserves the original meaning.
- **FR-007**: Body/paragraph text letter spacing MUST be increased from its
  current baseline sitewide.
- **FR-008**: Navigation link letter spacing MUST be increased from its
  current baseline (0.08em) by a clearly noticeable but subtle amount, not
  an extreme/drastic value.
- **FR-009**: All changes in this feature MUST preserve existing responsive
  behavior — no new horizontal scrolling, text wrapping/overflow, or
  layout breakage MUST be introduced at any previously supported
  breakpoint.
- **FR-010**: All visual changes MUST be reviewed against designer intent
  before being considered final, per this project's design-fidelity
  standard, since exact spacing/letter-spacing amounts are described
  qualitatively ("a little more," "a lot more, nothing drastic") rather
  than as precise values.

### Key Entities

*(Not applicable — this feature adjusts visual presentation of existing
static content and does not introduce or modify any data entities.)*

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: When shown the updated homepage side-by-side with the
  previous version, the designer confirms all four notes (underlay reveal,
  content/text-block padding and proportions, no em dashes and increased
  letter spacing, nav letter spacing) have been addressed to their
  satisfaction on the first review pass.
- **SC-002**: A sitewide text search finds zero em dash characters across
  all page content and metadata.
- **SC-003**: The homepage renders with no layout defects (no overlapping
  elements, no horizontal scroll, no text overflow/wrapping regressions)
  at desktop, tablet, and mobile breakpoints after the changes.
- **SC-004**: All four designer notes are implemented in a single review
  cycle with zero follow-up correction requests specifically about em
  dashes or nav letter spacing.

## Assumptions

- "A little more" underlay reveal and "a lot more, nothing drastic" nav
  letter spacing are qualitative directions; exact pixel/em values are left
  to implementation and MUST be confirmed with the designer before this
  feature is considered complete, per the project's Design Fidelity
  principle.
- The instruction to add more padding between the text block and the image
  underlay is understood as increasing breathing room around the overlap
  area (e.g., internal card padding and/or the gap outside the corner
  overlap), not eliminating the existing intentional overlap accent between
  the photo/backdrop and the text card entirely; this MUST be confirmed
  with the designer if the two adjustments (more underlay reveal vs. more
  separation from the text block) appear to conflict during implementation.
- "More letter spacing" in note 3 refers to body/paragraph text sitewide
  (distinct from the nav-specific increase called out separately in note
  4), since the notes explicitly separate the two.
- The em dash and letter-spacing rules apply to all current site pages
  (currently just the homepage) and are treated as an ongoing style rule
  for any pages added later (e.g., a future Work page), not a one-time
  cleanup limited to today's content.
- No new content, sections, or functionality are introduced by this
  feature; scope is limited to visual/typographic refinement of the
  existing landing page implementation delivered in `002-landing-page`.
- This feature does not change the site's color palette, imagery choices,
  fonts, or non-visual behavior — only spacing, proportions, letter
  spacing, and the removal of em dash characters.
