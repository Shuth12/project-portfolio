# Feature Specification: Services Page

**Feature Branch**: `006-services-page`

**Created**: 2026-08-22

**Status**: Draft

**Input**: User description: "Now we are going to work on the services page. I uploaded an image to follow exactly. Make the pattern image, Shelleycerny-blobs, the same size and look as the Shelleycerny-checkared image on the contact page. add a off white box with rounded corners and a strong drop shadow to the center then we will add a title to the top center of box, same style as the "Hi, I'm Shelley" at the top of the main page, that says "Services". from here we have a grid of 6 services that are all layed out like this; Icon on top, subtitle (style of subtitles on work pages), and a description in the body text style centered bellow that. in grid space 1 we have the ShelleyCerny_UXIcon image, subtitle UX/UI Design, body text "From wireframes to high fidelity designs, I create digital experiences that are intuitive, intentional, and beautiful." In grid space 2 we have the ShelleyCerny_BrandIcon image, subtitle "Brand Identity", and body text "Logo design, color palettes, typography, and all the pieces that make a brand feel cohesive and memorable." in grid box 3 we have the ShelleyCerny_PrintIcon image, subtitle "Print Design", body text "Business cards, letterheads, event materials, and beyond, Designed with the same attention to detail as any digital project." In grid box 4 we have the ShelleyCerny_SocialIcon image, sub title "Social Media Design", body text "On brand, scroll stopping content that actually connects with your audience." in grid box 5 we have the ShelleyCerny_WebIcon image, subtitle "Web Design", body text "Clean, user centered website designs that look great and feel effortless to navigate." in grid box 6 we have the ShelleyCerny_LetteringIcon image, sub title "Illustration & Hand Lettering", body text "Custom hand lettered signage, murals, and illustrated design elements with a personal touch."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Browse Shelley's service offerings (Priority: P1)

A prospective client or employer visits the Services page wanting to
understand the full range of design services Shelley offers, from UX/UI
design to hand lettering, so they can evaluate whether her skill set fits
their need.

**Why this priority**: This is the entire purpose of the page — without the
services grid rendering clearly and completely, the page provides no value
regardless of visual polish.

**Independent Test**: Load the Services page directly in a browser and
confirm all six services (icon, subtitle, and description) are visible and
readable in the grid.

**Acceptance Scenarios**:

1. **Given** a visitor loads the Services page, **When** the page finishes
   loading, **Then** they see the site header/nav, a full-width background
   pattern, a centered off-white card titled "Services", and a 6-item grid of
   services, matching the reference mockup's layout and palette.
2. **Given** a visitor on the Services page, **When** they view the services
   grid, **Then** each of the six grid items displays its icon on top, a
   subtitle below the icon, and a centered description below the subtitle, in
   the order: UX/UI Design, Brand Identity, Print Design, Social Media
   Design, Web Design, Illustration & Hand Lettering.
3. **Given** a visitor on a mobile-width viewport, **When** they load the
   Services page, **Then** the card, title, and all six grid items remain
   fully visible and readable with no overlapping or cut-off content.

---

### User Story 2 - Navigate to the Services page from anywhere on the site (Priority: P2)

A visitor on the landing page, Work gallery, a project detail page, or the
Contact page wants to reach the Services page via the header navigation.

**Why this priority**: Supporting navigation — the Services page must be
reachable consistently from the site-wide header already established across
the site, but this is secondary to the page itself rendering correctly.

**Independent Test**: From any existing page, click "Services" in the header
nav and confirm it lands on the Services page.

**Acceptance Scenarios**:

1. **Given** a visitor on any page of the site, **When** they click
   "Services" in the header navigation, **Then** they land on the Services
   page.
2. **Given** a visitor on the Services page, **When** they view the page,
   **Then** the same site header (logo, nav) and footer used elsewhere on
   the site are present and consistent.

---

### Edge Cases

- How does the 6-item grid reflow at narrow (≤375px) and wide (≥1440px)
  viewports, given the mockup shows a 3-column grid at desktop width? At
  minimum, the grid must remain readable and non-overlapping at all
  supported widths, per FR-011.
- What happens when a visitor navigates directly to the Services page URL
  without going through the nav first? The page must still render correctly
  with its own header, footer, and full services grid.
- What happens to the two-line subtitles ("Social Media Design",
  "Illustration & Hand Lettering") at narrower widths where they may wrap
  differently than in the mockup? Wrapping may reflow but must not overlap
  or clip adjacent grid items.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The Services page MUST display the same site header (logo,
  "About"/"Work"/"Contact"/"Services" navigation) and footer ("Designed by:
  Shelley Cerny") used elsewhere on the site, so navigation and branding
  stay consistent.
- **FR-002**: The Services page's header "Services" navigation link, on
  every page of the site, MUST point to this Services page (replacing the
  existing placeholder destination).
- **FR-003**: The Services page MUST display a full-width background pattern
  using the `Shelleycerny-blobs` image, sized and presented consistently
  with the `Shelleycerny-checkared` background pattern already used on the
  Contact page.
- **FR-004**: The Services page MUST display a centered off-white content
  card with rounded corners and a strong drop shadow, matching the reference
  mockup (`assets/page_mockups/ShelleyCerny_Website_Services.png`).
- **FR-005**: The content card MUST display the heading "Services" at its
  top center, styled consistently with the "Hi I'm Shelley," heading on the
  landing page.
- **FR-006**: The content card MUST display a 6-item grid of services below
  the heading, arranged 3 columns by 2 rows at desktop width, matching the
  reference mockup.
- **FR-007**: Each of the 6 grid items MUST display, top to bottom: a
  service icon image, a subtitle styled consistently with the project
  subtitle style used on Work page project-detail pages, and a description
  in the site's standard body text style, horizontally centered.
- **FR-008**: The 6 grid items MUST use the following content, in this
  order:
  1. Icon `ShelleyCerny_UXIcon`, subtitle "UX/UI Design", description "From
     wireframes to high fidelity designs, I create digital experiences that
     are intuitive, intentional, and beautiful."
  2. Icon `ShelleyCerny_BrandIcon`, subtitle "Brand Identity", description
     "Logo design, color palettes, typography, and all the pieces that make
     a brand feel cohesive and memorable."
  3. Icon `ShelleyCerny_PrintIcon`, subtitle "Print Design", description
     "Business cards, letterheads, event materials, and beyond. Designed
     with the same attention to detail as any digital project."
  4. Icon `ShelleyCerny_SocialIcon`, subtitle "Social Media Design",
     description "On brand, scroll stopping content that actually connects
     with your audience."
  5. Icon `ShelleyCerny_WebIcon`, subtitle "Web Design", description "Clean,
     user centered website designs that look great and feel effortless to
     navigate."
  6. Icon `ShelleyCerny_LetteringIcon`, subtitle "Illustration & Hand
     Lettering", description "Custom hand lettered signage, murals, and
     illustrated design elements with a personal touch."
- **FR-009**: Every service icon MUST include descriptive `alt` text
  identifying the service it represents.
- **FR-010**: The Services page MUST remain fully usable and readable on
  both desktop and mobile viewports using CSS-based responsive layout, with
  no animated or motion-based transitions, consistent with the site's
  no-motion principle.
- **FR-011**: On narrower viewports, the services grid MUST reflow (e.g. to
  fewer columns) rather than shrinking content to the point of
  illegibility or causing horizontal overflow.
- **FR-012**: The Services page's layout, color palette, and typography
  MUST visually match the reference mockup, consistent with the palette and
  typography already established across the rest of the site.

### Key Entities

- **Services Page**: A single static page presenting a title and a fixed
  list of six services (icon, subtitle, description each) — no forms, no
  submitted data, no backend, no per-service links.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A visitor can view all six of Shelley's service offerings
  (icon, title, and description) without any content being cut off or
  hidden, within one page load.
- **SC-002**: The Services page renders without layout breakage (no
  overlapping or cut-off content) at common breakpoints (~375px, ~768px,
  ~1440px viewport widths).
- **SC-003**: The implemented Services page matches the reference mockup's
  layout, color palette, and typography with no unresolved visual
  deviations.
- **SC-004**: The "Services" nav link resolves to the Services page from
  every existing page on the site, with zero broken links.

## Assumptions

- The Services page is a new static page at the site root
  (`services.html`), consistent with the existing `index.html`/`work.html`/
  `contact.html` file structure — no build step or templating engine is
  introduced.
- The grid items are static/informational only; per the mockup, no icon or
  grid item links elsewhere (e.g. to Work or Contact) — that is out of scope
  for this feature.
- The existing `Shelleycerny-blobs` pattern image and the six
  `ShelleyCerny_*Icon` images are used as provided, with no new image
  processing required.
- Reuses the same header, footer, fonts, and color tokens already
  implemented for the landing, Work, and Contact pages, rather than
  introducing new site chrome.
- The minor wording difference between the user's dictated body text for
  Print Design ("... and beyond, Designed with the same attention...") and
  the reference mockup image ("... and beyond. Designed with the same
  attention...") is treated as a punctuation/capitalization typo; the
  mockup's phrasing is used as the source of truth per FR-008 item 3.
- The Web Design grid item's body text in the reference mockup image is
  identical to the Social Media Design item's text ("On brand, scroll
  stopping content that actually connects with your audience."), which
  reads as a leftover placeholder/copy-paste artifact in the mockup rather
  than intentional duplication. The user's explicit dictated text for Web
  Design ("Clean, user centered website designs that look great and feel
  effortless to navigate.") is treated as the source of truth per FR-008
  item 5, since it is distinct, specific, and was typed out in full by the
  user rather than inferred from the image.
