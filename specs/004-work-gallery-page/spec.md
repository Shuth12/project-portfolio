# Feature Specification: Work Gallery Page

**Feature Branch**: `004-work-gallery-page`

**Created**: 2026-08-20

**Status**: Draft

**Input**: User description: "The about page/landing page is done I want to move on to the work page that will display the work I have done and let you click on the thumbnails and it brings you to the specific portfolio page that shows that project. Follow the @assets/page_mockups/ShelleyCerny_WebsiteWork.jpg I want it to match this will all of the assets I have provided."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Browse the project thumbnail grid (Priority: P1)

A prospective client, recruiter, or peer navigates to the Work page and wants
to quickly scan Shelley's range of design work as a visual grid, without
reading through paragraphs of text.

**Why this priority**: This is the core purpose of the Work page per the
PRD's "Portfolio / Work Gallery" section — visitors need to see the breadth
of work at a glance before deciding what to look at more closely.

**Independent Test**: Load the Work page in a browser and confirm all
project thumbnails render in a grid matching the reference mockup, each with
a recognizable image representing that project.

**Acceptance Scenarios**:

1. **Given** a visitor loads the Work page, **When** the page finishes
   loading, **Then** they see the site header/nav, a grid of project
   thumbnails matching the reference mockup's layout and project set, and
   the site footer.
2. **Given** a visitor on a mobile-width viewport, **When** they load the
   Work page, **Then** the thumbnail grid reflows into fewer columns and
   every thumbnail remains fully visible and readable, with no overlapping
   or cut-off images.

---

### User Story 2 - Open a project's detail page from its thumbnail (Priority: P1)

A visitor sees a thumbnail for a project that interests them and clicks it
to see more of that specific project's work.

**Why this priority**: This is the explicit behavior requested — the
thumbnail grid is only useful if it leads somewhere; without working
click-through, the Work page is a dead end.

**Independent Test**: Click each thumbnail on the Work page and confirm it
navigates to a distinct page showing that project's own images and no other
project's images.

**Acceptance Scenarios**:

1. **Given** a visitor on the Work page, **When** they click a project
   thumbnail, **Then** they are taken to that project's own detail page
   showing additional images/mockups for that project.
2. **Given** a visitor on a project detail page, **When** they look at the
   images shown, **Then** every image belongs to that project only (no
   mixing of projects on one detail page).
3. **Given** a visitor on a project detail page, **When** they want to see
   other work, **Then** a link back to the Work gallery is available and
   returns them to the full thumbnail grid.

---

### User Story 3 - Navigate to the Work page from anywhere on the site (Priority: P2)

A visitor on the landing page (or a project detail page) wants to reach the
Work gallery via the header navigation.

**Why this priority**: Supporting navigation — the Work page must be
reachable consistently from the site-wide header already established on the
landing page, but this is secondary to the gallery and detail pages
themselves working correctly.

**Independent Test**: From the landing page, click "Work" in the header nav
and confirm it lands on the Work gallery page; from a project detail page,
confirm the same header nav is present and functional.

**Acceptance Scenarios**:

1. **Given** a visitor on any page of the site, **When** they click "Work"
   in the header navigation, **Then** they land on the Work gallery page.
2. **Given** a visitor on a project detail page, **When** they view the
   page, **Then** the same site header (logo, nav) and footer used on the
   landing page and Work gallery are present and consistent.

---

### Edge Cases

- What happens when a project's thumbnail image fails to load? Meaningful
  `alt` text must still identify the project.
- How does the 5-column grid shown in the mockup reflow at narrow
  (≤375px) and wide (≥1440px) viewports, given it cannot stay 5 columns
  wide on a phone screen?
- What happens when a visitor navigates directly to a project detail page
  URL without going through the grid first? The page must still render
  correctly with its own header, images, and back-to-Work link.
- What happens when a visitor navigates the grid or a detail page using
  only a keyboard? Every thumbnail and the back-to-Work link must be
  reachable and clearly focusable without a mouse.
- What happens when a project has only one supporting image beyond its
  thumbnail? The detail page layout must not look broken or sparse with a
  minimal image set.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The Work page MUST display the same site header (logo,
  "About"/"Work"/"Contact"/"Services" navigation) and footer
  ("Designed by: Shelley Cerny") used on the landing page, so navigation
  and branding stay consistent across the site.
- **FR-002**: The Work page MUST display a grid of project thumbnails
  matching the reference mockup's layout, one thumbnail per project, using
  each project's existing `*_MockUp_Thumbnail.*` image asset already present
  in the repository under `assets/images/<project>/`.
- **FR-003**: The Work page MUST feature the following ten projects, in the
  order shown in the reference mockup: The Yoga Space, Red Cedar Coffee,
  Bouncy, Go Pint, Boyd Consulting, Invitations, Fit4Mom, Book, Wedding
  Signage & Stationery, and Murals.
- **FR-004**: Each project thumbnail MUST be a standard HTML link (`<a>`
  tag) that navigates to that project's own detail page, so the grid is
  fully usable via plain HTML navigation with no JavaScript required.
- **FR-005**: Each project MUST have its own detail page displaying that
  project's supporting images from its `assets/images/<project>/` folder
  (excluding the thumbnail image itself, which is only used on the Work
  grid), along with the project's title.
- **FR-006**: Each project detail page MUST include a link back to the Work
  gallery page.
- **FR-007**: The Work page and all project detail pages MUST remain fully
  usable and readable on both desktop and mobile viewports using CSS-based
  responsive layout, with no animated or motion-based transitions (per the
  constitution's no-motion principle) and no JavaScript-based filtering or
  lightbox behavior.
- **FR-008**: All images on the Work page and project detail pages MUST
  include descriptive `alt` text identifying the project and, where
  relevant, the specific piece of work shown.
- **FR-009**: The Work page's layout, color palette, and typography MUST
  visually match the reference mockup
  (`assets/page_mockups/ShelleyCerny_WebsiteWork.jpg`), consistent with the
  palette and typography already established on the landing page (cream
  background, teal panel, mustard-yellow footer accent, existing site
  typeface).
- **FR-010**: The animated project asset
  (`assets/images/bouncy/Bouncy_Logo_Bounce.gif`), if used on the Bouncy
  project's detail page, MUST be displayed as originally provided per the
  constitution's portfolio-content exception, and MUST NOT be used as the
  Work grid thumbnail for that project (the grid uses the static
  `Bouncy_MockUp_Thumbnail.jpg` per FR-002).
- **FR-011**: The file/content structure for the Work page and project
  detail pages MUST allow a new project to be added (new folder of images
  plus one new detail page and one new grid entry) without modifying shared
  layout or CSS files, per the constitution's content-updatability
  principle.

### Key Entities

- **Project**: A single body of design work (e.g., "The Yoga Space", "Red
  Cedar Coffee") with a title, one thumbnail image used on the Work grid,
  and a set of one or more supporting images shown on its own detail page.
- **Work Grid**: The ordered collection of all ten Projects, displayed as
  thumbnails on the Work page.
- **Project Detail Page**: A dedicated page per Project showing its title,
  supporting images, and a link back to the Work Grid.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A visitor can see thumbnails for all ten projects on the Work
  page without any additional clicks after the page loads.
- **SC-002**: Clicking any project thumbnail navigates to that project's own
  detail page 100% of the time, with zero console errors.
- **SC-003**: Every project detail page shows only images belonging to that
  project, and includes a working link back to the Work gallery.
- **SC-004**: The Work page and project detail pages render without layout
  breakage (no overlapping or cut-off content) at common breakpoints
  (~375px, ~768px, ~1440px viewport widths).
- **SC-005**: The implemented Work page matches the reference mockup's
  layout, color palette, and typography with no unresolved visual
  deviations, other than the ten confirmed projects and their existing
  asset filenames.

## Assumptions

- The ten project tiles visible in
  `assets/page_mockups/ShelleyCerny_WebsiteWork.jpg` correspond one-to-one,
  in the same left-to-right, top-to-bottom order, with the ten project
  asset folders already in the repository that each contain a
  `*_MockUp_Thumbnail.*` file: `yoga_space`, `red_cedar`, `bouncy`,
  `go_pints`, `boyd`, `invitations`, `fit_for_mom`, `book`, `wedding_sign`,
  and `murals`. This mapping is based on matching each folder's thumbnail
  image content to the corresponding tile in the mockup.
- Project display titles ("The Yoga Space", "Red Cedar Coffee", "Bouncy",
  "Go Pint", "Boyd Consulting", "Invitations", "Fit4Mom", "Book",
  "Wedding Signage & Stationery", "Murals") are working titles derived from
  each folder's name and the logos/mockups shown within it. Shelley can
  refine exact copy/titles later without touching layout or CSS, per the
  constitution's content-updatability principle.
- The `assets/images/logo/` folder (the site's own wordmark) and the
  `assets/images/flower_baby/` folder (a single supporting invitation image
  with no thumbnail of its own) are not separate Work grid entries. The
  `flower_baby` image is treated as an additional supporting image on the
  Invitations project's detail page, since it depicts an invitation design
  and has no dedicated thumbnail or grid tile in the mockup.
- Each project detail page is a new, individual static HTML page (e.g.,
  `work/the-yoga-space.html`), consistent with the PRD's Open Question on
  portfolio structure now being resolved by this spec in favor of one
  detail page per project (rather than a single long scrolling gallery).
  This spec does not prescribe a specific file/folder naming convention
  beyond "one page per project reachable from the grid"; the implementer
  may choose the convention (e.g., a `work/` subfolder) that best satisfies
  FR-011.
- No project filtering, search, tags/categories, or lightbox/modal image
  viewer is in scope for this spec — the mockup shows a plain thumbnail
  grid, and the constitution favors plain `<a>`-based navigation over added
  JavaScript interactivity unless a design explicitly calls for it.
- Consistent with the landing page spec, the "Contact" and "Services" nav
  links remain placeholder destinations (`#`) on the Work page and project
  detail pages until those features are scoped separately.
- Project detail pages reuse the same header, footer, fonts, and color
  tokens already implemented for the landing page, rather than introducing
  new site chrome, since the mockup shows the same header/footer treatment
  on the Work page as on the About/landing mockup.
