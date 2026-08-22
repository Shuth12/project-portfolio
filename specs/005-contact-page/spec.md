# Feature Specification: Contact Page

**Feature Branch**: `005-contact-page`

**Created**: 2026-08-22

**Status**: Draft

**Input**: User description: "Now we are going to work on the contact page. please referance the image ia attached here and make the page look exactly like this the pattern image is called shelleycerny-checkared and that will be the same size as the off white box on all work tumbnail page. the is another off white box in the center with a drop shadow that will be overlayed with the image ShelleyCerny_Photo02 to the right with a drop shadow. to the left but still in the box will be the title "Say Hello!" in the style as "Hi, I'm Shelley Cerny" on the main page. then bellow, indented and with generous padding between the edge of the box and the image on the right in body text put "Whether you are looking for a UX/UI designer, need a brand identity refresh, or just want to talk design, I would love to hear from you. I am currently open to remote junior UX/UI design roles and freelance projects. Reach out and let's see what we can make together." then bellow that put a botton, same style as the "Download my resume" buttom on the main page, that says "Send Me An Email". When pressed the button will navigate to their mail app with a new message and my email prefilled in, shelley.cerny@gmail.com."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Reach out via email from the Contact page (Priority: P1)

A prospective employer, client, or peer visits the Contact page wanting to
get in touch with Shelley about work opportunities or design collaboration,
and needs a fast, frictionless way to start an email conversation.

**Why this priority**: This is the entire purpose of the page — without a
working way to initiate contact, the page provides no value regardless of
how well it matches the visual design.

**Independent Test**: Load the Contact page directly in a browser and click
the "Send Me An Email" button; confirm it opens the visitor's default mail
client with a new message addressed to Shelley's email.

**Acceptance Scenarios**:

1. **Given** a visitor loads the Contact page, **When** the page finishes
   loading, **Then** they see the site header/nav, the "Say Hello!" message
   and supporting body text, a photo of Shelley, and a "Send Me An Email"
   button, matching the reference mockup's layout and palette.
2. **Given** a visitor on the Contact page, **When** they click "Send Me An
   Email", **Then** their device's default mail application opens a new
   message pre-addressed to shelley.cerny@gmail.com.
3. **Given** a visitor on a mobile-width viewport, **When** they load the
   Contact page, **Then** the card, photo, text, and button remain fully
   visible and readable with no overlapping or cut-off content.

---

### User Story 2 - Navigate to the Contact page from anywhere on the site (Priority: P2)

A visitor on the landing page, Work gallery, or a project detail page wants
to reach the Contact page via the header navigation.

**Why this priority**: Supporting navigation — the Contact page must be
reachable consistently from the site-wide header already established across
the site, but this is secondary to the page itself working correctly.

**Independent Test**: From any existing page, click "Contact" in the header
nav and confirm it lands on the Contact page.

**Acceptance Scenarios**:

1. **Given** a visitor on any page of the site, **When** they click
   "Contact" in the header navigation, **Then** they land on the Contact
   page.
2. **Given** a visitor on the Contact page, **When** they view the page,
   **Then** the same site header (logo, nav) and footer used elsewhere on
   the site are present and consistent.

---

### Edge Cases

- What happens when a visitor's device has no email application configured?
  The `mailto:` link still degrades gracefully per standard browser/OS
  behavior (e.g., prompting to choose or set up a mail handler); no custom
  fallback UI is in scope.
- How does the card + photo overlay layout reflow at narrow (≤375px) and
  wide (≥1440px) viewports, given the mockup shows the photo overlapping the
  right edge of the card at desktop width?
- What happens when a visitor navigates the page using only a keyboard? The
  "Send Me An Email" button must be reachable and clearly focusable without
  a mouse.
- What happens when a visitor navigates directly to the Contact page URL
  without going through the nav first? The page must still render correctly
  with its own header, footer, and working button.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The Contact page MUST display the same site header (logo,
  "About"/"Work"/"Contact"/"Services" navigation) and footer ("Designed by:
  Shelley Cerny") used elsewhere on the site, so navigation and branding
  stay consistent.
- **FR-002**: The Contact page's header "Contact" navigation link, on every
  page of the site, MUST point to this Contact page (replacing the existing
  placeholder destination).
- **FR-003**: The Contact page MUST display a full-width background pattern
  using the `Shelleycerny-checkared` image, sized to match the width of the
  off-white content box used on the Work gallery page.
- **FR-004**: The Contact page MUST display a centered off-white content
  card with a drop shadow, matching the reference mockup
  (`assets/page_mockups/ShelleyCerny_Website_Contact.png`).
- **FR-005**: The content card MUST display Shelley's photo
  (`ShelleyCerny_Photo02`) overlapping the right side of the card with its
  own drop shadow, per the reference mockup.
- **FR-006**: The content card MUST display the heading "Say Hello!" styled
  consistently with the "Hi, I'm Shelley Cerny" heading on the landing page.
- **FR-007**: The content card MUST display body copy (provided in the
  Input above) positioned to the left of the photo, with generous padding
  between the card's edge and the photo.
- **FR-008**: The content card MUST include a "Send Me An Email" button
  styled consistently with the "Download My Resume" button on the landing
  page.
- **FR-009**: Clicking/activating the "Send Me An Email" button MUST open
  the visitor's default email client with a new message addressed to
  shelley.cerny@gmail.com, using a standard `mailto:` link so the page
  remains fully static with no JavaScript or backend required.
- **FR-010**: The Contact page MUST remain fully usable and readable on both
  desktop and mobile viewports using CSS-based responsive layout, with no
  animated or motion-based transitions, consistent with the site's no-motion
  principle.
- **FR-011**: The photo on the Contact page MUST include descriptive `alt`
  text identifying Shelley.
- **FR-012**: The Contact page's layout, color palette, and typography MUST
  visually match the reference mockup, consistent with the palette and
  typography already established across the rest of the site.

### Key Entities

- **Contact Page**: A single static page presenting a greeting, brief bio
  invitation, and a single call-to-action (email) — no form fields, no
  submitted data, no backend.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A visitor can locate a way to contact Shelley and trigger an
  email to her within one click of loading the Contact page.
- **SC-002**: Clicking the "Send Me An Email" button opens a pre-addressed
  email draft 100% of the time, with zero console errors.
- **SC-003**: The Contact page renders without layout breakage (no
  overlapping or cut-off content) at common breakpoints (~375px, ~768px,
  ~1440px viewport widths).
- **SC-004**: The implemented Contact page matches the reference mockup's
  layout, color palette, and typography with no unresolved visual
  deviations.
- **SC-005**: The "Contact" nav link resolves to the Contact page from every
  existing page on the site, with zero broken links.

## Assumptions

- The Contact page is a new static page at the site root (e.g.,
  `contact.html`), consistent with the existing `index.html`/`work.html`
  file structure — no build step or templating engine is introduced.
- No contact form, validation, or message storage is in scope; per the
  project constitution, contact is a `mailto:` link only.
- The email subject/body are left blank in the generated draft unless
  refined later; the requirement is only that the recipient address is
  pre-filled.
- The "Services" nav link remains a placeholder destination (`#`) since it
  is out of scope for this feature.
- The existing `Shelleycerny-checkared` pattern image and `ShelleyCerny_Photo02`
  image are used as provided, with no new image processing required.
- Reuses the same header, footer, fonts, and color tokens already
  implemented for the landing page and Work gallery, rather than
  introducing new site chrome.
