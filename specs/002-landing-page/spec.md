# Feature Specification: Landing Page (Home / About)

**Feature Branch**: `002-landing-page`

**Created**: 2026-08-18

**Status**: Draft

**Input**: User description: "Lets start with the landing page use @assets/page_mockups/ShelleyCerny_WebsiteAbout.jpg as a reference please ask questions where needed"

## Clarifications

### Session 2026-08-18

- Q: Is there an actual headshot photo of Shelley ready to add to the repo for the hero section, or should implementation use a placeholder image until one is supplied? → A: Not yet — placeholder. Reference a placeholder path (e.g. `assets/images/profile/ShelleyCerny-Headshot.jpg`) to be dropped in later, same pattern as the resume file.
- Q: The mockup shows a hand-lettered, script-style "Shelley Cerny" logo. Should the site logo be an image asset, or styled text using a web font? → A: Placeholder image asset (e.g. `assets/images/logo/ShelleyCerny-Logo.svg`), since it's a custom hand-drawn mark that can't be recreated with a standard web font.
- Q: The mockup uses a bold block/uppercase font for nav and headings plus a hand-lettered script for the logo. Do you have licensed font files to use, or should the implementer pick close free alternatives? → A: Free equivalents — select closely-matching free/open web fonts (e.g. Google Fonts) that approximate the mockup's bold block headings, no licensing cost or risk.
- Q: If a color pairing in the mockup doesn't meet accessibility contrast guidelines, which wins — design fidelity or accessibility? → A: Design fidelity wins — match the mockup's exact colors as given even where contrast is borderline; treat it as an accepted tradeoff, not a deviation to flag.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Learn who Shelley is (Priority: P1)

A prospective client, recruiter, or peer arrives at the site's homepage and wants to quickly understand who Shelley is, what she does, and whether she's a fit for their needs — without navigating to a separate "About" page.

**Why this priority**: This is the core purpose of the landing page per the PRD: the home page absorbs the About content directly, so visitors must be able to get a full picture of Shelley (photo, name, role, bio) the moment they land.

**Independent Test**: Load the landing page in a browser and confirm a visitor can read Shelley's name, tagline/role, and biography without clicking anything.

**Acceptance Scenarios**:

1. **Given** a visitor loads the landing page, **When** the page finishes loading, **Then** they see a photo of Shelley, the heading "Hi I'm Shelley," and a biography paragraph describing her background and what she's looking for.
2. **Given** a visitor on a mobile-width viewport, **When** they load the landing page, **Then** the photo and bio text remain fully readable and are not cut off or overlapping.

---

### User Story 2 - Download Shelley's resume (Priority: P2)

A recruiter or hiring manager reading the bio wants a copy of Shelley's resume to review or forward internally.

**Why this priority**: The mockup's primary call-to-action on the page is the "Download My Resume" button — it is the single most important next action the page offers a hiring-focused visitor.

**Independent Test**: Click the "Download My Resume" button and confirm it opens or downloads a resume file.

**Acceptance Scenarios**:

1. **Given** a visitor viewing the landing page, **When** they click "Download My Resume," **Then** the resume file opens or downloads successfully.

---

### User Story 3 - Navigate to other parts of the site (Priority: P3)

A visitor who has read the bio wants to see Shelley's work, get in touch, or explore other sections of the site via the header navigation.

**Why this priority**: Navigation is supporting functionality — useful once a visitor is oriented, but secondary to the bio content itself landing correctly.

**Independent Test**: Click each header navigation link and confirm it takes the visitor to the expected destination (a page, section, or anchor) without a broken/dead link.

**Acceptance Scenarios**:

1. **Given** a visitor on the landing page, **When** they click "About," **Then** they are scrolled to the bio section on the same page.
2. **Given** a visitor on the landing page, **When** they click "Work," "Contact," or "Services," **Then** they are taken to the corresponding page/placeholder without a console error, understanding that those destinations may not have real content until their own specs are implemented.

---

### Edge Cases

- What happens when the resume file is missing or fails to load? The download button should not silently fail; the page must not error out.
- What happens when Shelley's headshot photo (currently a placeholder path) fails to load? Meaningful `alt` text should still convey the content.
- How does the layout behave on very narrow (≤375px) and very wide (≥1440px) viewports, given the mockup's fixed two-column hero composition?
- What happens when a visitor navigates with JavaScript disabled? Since the PRD requires no server/backend and JS only for genuinely necessary interactivity, all navigation and content on this page must work without JavaScript.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The landing page MUST display a header containing the "Shelley Cerny" site logo/wordmark and a navigation menu with links labeled About, Work, Contact, and Services, matching the order shown in the reference mockup. The logo MUST be implemented as an image asset (not CSS-styled text), referencing a placeholder path (e.g. `assets/images/logo/ShelleyCerny-Logo.svg`) until the real hand-lettered logo file is supplied.
- **FR-002**: The landing page MUST display an introduction/hero section containing a photo of Shelley, referencing a placeholder image path (e.g. `assets/images/profile/ShelleyCerny-Headshot.jpg`) until a real headshot photo is supplied.
- **FR-003**: The landing page MUST display the heading "Hi I'm Shelley," followed by a biography paragraph covering her background, design focus, and what kind of role she's seeking, matching the content and tone of the reference mockup.
- **FR-004**: The landing page MUST provide a "Download My Resume" call-to-action that lets a visitor open or download Shelley's resume file.
- **FR-005**: The landing page MUST display a footer with the attribution text "Designed by: Shelley Cerny."
- **FR-006**: The landing page's layout, color palette (cream background, teal panel, mustard-yellow accent shapes, green headings/logo, purple button), and typography MUST visually match the reference mockup, per the PRD's design fidelity requirement. Typography MUST use free/open web fonts (e.g. Google Fonts) chosen to closely approximate the mockup's bold block heading/nav style, since no licensed font files are being supplied. Where a mockup color pairing has borderline accessibility contrast, the mockup's exact color MUST be used as-is (design fidelity takes precedence over contrast in this case) rather than substituted or flagged as a deviation.
- **FR-007**: The landing page MUST remain fully usable and readable on both desktop and mobile viewports using CSS-based responsive layout, with no animated or motion-based transitions.
- **FR-008**: All images on the landing page MUST include descriptive `alt` text.
- **FR-009**: All navigation links and the resume download link MUST be implemented as standard HTML links (`<a>` tags) so the page works with plain HTML navigation. The "About" anchor MUST resolve within this page; "Work," "Contact," "Services," and the resume download are expected to point to placeholder destinations (per FR-011–FR-014) until their respective content is added in future work.
- **FR-010**: The "About" navigation link MUST be an in-page anchor that returns the visitor to the top/bio section of the landing page, since that section is the site's About content per the PRD.
- **FR-011**: The "Work" navigation link MUST point to `work.html`, even though that page is not yet built as part of this spec; it will resolve once the Work gallery feature is implemented in a future spec.
- **FR-012**: The "Services" navigation link MUST be included in the header per the mockup, pointing to a placeholder destination (e.g. `#` or `services.html`) to be resolved when a Services page/section is scoped in a future spec.
- **FR-013**: The "Download My Resume" button MUST link to a placeholder resume file path (e.g. `assets/resume/ShelleyCerny-Resume.pdf`) so the button is visually and structurally complete even though the actual PDF has not yet been supplied; the link target is expected to 404 until the file is added to the repository.
- **FR-014**: The "Contact" navigation link MUST point to a placeholder destination (`#`), matching the same treatment as "Services," to be resolved when the Contact feature is scoped in a future spec.

### Key Entities

- **Bio Content**: Shelley's name, role/tagline, headshot photo, and biography paragraph displayed on the landing page.
- **Resume File**: A downloadable document linked from the "Download My Resume" call-to-action.
- **Navigation Menu**: The set of header links (About, Work, Contact, Services) presented on every page, defined here for the landing page's header.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A visitor can read Shelley's name, role, and full biography without any additional clicks or navigation after the page loads.
- **SC-002**: The "About" in-page anchor works on 100% of clicks with zero console errors; the "Work," "Contact," "Services" nav links and resume download link point to their agreed placeholder destinations with zero console errors, even though those destinations don't yet resolve to real content.
- **SC-003**: The page renders without layout breakage (no overlapping or cut-off content) at common breakpoints (~375px, ~768px, ~1440px viewport widths).
- **SC-004**: The implemented page matches the reference mockup's layout, color palette, and typography with no unresolved visual deviations, other than the agreed placeholder assets (headshot, logo) and the free-font typography approximation.
- **SC-005**: The resume download completes in under 2 seconds on a standard broadband connection.

## Assumptions

- The reference mockup labeled "WebsiteAbout.jpg" represents the site's Home/Landing page, since the PRD (`docs/PRD.md` §3, §5) explicitly states there is no separate About page and that bio/introduction content lives on the Home/Landing page instead.
- This spec covers only the landing page itself (header, hero/bio section, footer). The Work gallery and Contact pages referenced by the header navigation are separate, not-yet-built features covered by future specs.
- The site logo/wordmark is treated as a static image asset matching the hand-lettered "Shelley Cerny" logotype shown in the mockup; no interactive branding behavior is implied.
- Per the PRD, no animations or motion-based transitions are used anywhere on this page, including hover/focus states, which are implemented with simple CSS pseudo-classes rather than transitions.
- The page is implemented as static HTML/CSS (JavaScript only if a specific interaction genuinely requires it), consistent with the PRD's static-site constraint and GitHub Pages hosting target.
- "Work," "Services," and the resume download link point to placeholder destinations (`work.html`, a `services.html`/`#` placeholder, and `assets/resume/ShelleyCerny-Resume.pdf` respectively) that are not expected to resolve to real content or files as part of this spec; they will be completed by future specs (Work page) or when Shelley supplies the resume PDF.
- A "Services" page/section is not part of the PRD's approved site structure (Home/Landing, Work, Contact); its nav entry is included to match the mockup visually but its actual scope is undecided and deferred.
- Shelley's headshot photo has not yet been supplied; the hero section references a placeholder image path to be filled in later, following the same pattern as the resume file.
- The hand-lettered "Shelley Cerny" logo has not yet been supplied as a usable web asset; the header references a placeholder image path until the real logo file is added.
- No licensed font files are being supplied for this spec; free/open web fonts (e.g. Google Fonts) will be chosen to closely approximate the mockup's bold block heading/nav typography.
- Where the mockup's exact colors produce borderline accessibility contrast, design fidelity takes precedence over the constitution's general contrast guidance for this spec; such pairings are an accepted tradeoff, not a flagged deviation.
