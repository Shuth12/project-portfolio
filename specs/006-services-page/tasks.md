---

description: "Task list template for feature implementation"
---

# Tasks: Services Page

**Input**: Design documents from `/specs/006-services-page/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/page-contract.md, quickstart.md

**Tests**: Not requested for this feature. Validation is manual, via `quickstart.md`'s 6 scenarios (Polish phase runs them).

**Organization**: Tasks are grouped by user story (US1, US2 from spec.md) to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (US1, US2)
- File paths are exact and relative to the repository root unless noted

## Path Conventions

Static multi-page site, no `src/`/`tests/` split — see plan.md's Project
Structure. The new file lives at `services.html` (repo root);
`assets/css/styles.css` is extended in place. All source images already
exist under `assets/images/`.

**Note on relative paths**: root-level pages (`index.html`, `work.html`,
`contact.html`) link to the new page as `services.html`; pages under
`work/` link to it as `../services.html`, matching the existing
relative-path convention used for `work.html`/`contact.html`/
`index.html#bio` links on those pages.

---

## Phase 1: Setup

**Purpose**: Confirm prerequisites before the page is authored

- [X] T001 Verify `assets/images/Shelleycerny-blobs.png`, `assets/images/ShelleyCerny_UXIcon.png`, `assets/images/ShelleyCerny_BrandIcon.png`, `assets/images/ShelleyCerny_PrintIcon.png`, `assets/images/ShelleyCerny_SocialIcon.png`, `assets/images/ShelleyCerny_WebIcon.png`, and `assets/images/ShelleyCerny_LetteringIcon.png` all exist on disk; note and resolve any mismatch before continuing

**Checkpoint**: All source assets confirmed present

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Shared CSS that User Story 1's page depends on

**⚠️ CRITICAL**: Complete before starting Phase 3

- [X] T002 Add `.services-main`, `.services-pattern`, and `.services-card` rules to `assets/css/styles.css`: `.services-pattern` reuses `.contact-pattern`'s properties exactly (`max-width: 75rem`, centered, `1.5rem` border radius, `background-repeat: no-repeat`, `background-position: center`, `background-size: cover`) but with `background-image: url("../images/Shelleycerny-blobs.png")` per `research.md`'s background-pattern decision; `.services-card` is an off-white, rounded-corner card reusing `.contact-card`'s `border-radius: 1.5rem` and two-layer `box-shadow` value for a strong drop shadow, but without `.contact-card`'s flex/photo-overlap layout (stack heading + grid vertically instead), centered within `.services-pattern`
- [X] T003 Add a `.services-card h1` rule to `assets/css/styles.css` matching `.hero-card h1`'s property values (font-family, font-weight, color, font-size, letter-spacing, uppercase text-transform) per `research.md`'s heading-style decision, centered at the top of the card
- [X] T004 Add `.services-grid` and `.service-item` rules to `assets/css/styles.css`: `.services-grid` is a CSS Grid with 3 columns at desktop width (reflowing to 2 then 1 column at the file's existing `64rem`/`48rem`/`23.5rem` breakpoints per FR-011); `.service-item` center-aligns its icon, then a subtitle reusing `.project-subtitle`'s font/size/color/letter-spacing values, then a description reusing `.project-body`'s font/size/color values, stacked top to bottom per FR-007

**Checkpoint**: Shared services-page CSS classes exist — User Story 1 can now be authored against them

---

## Phase 3: User Story 1 - Browse Shelley's service offerings (Priority: P1) 🎯 MVP

**Goal**: A visitor loads `services.html` and sees the "Services" heading and all six services (icon, subtitle, description) laid out in a 3x2 grid inside the off-white card.

**Independent Test**: Load `services.html` directly in a browser, visually confirm it matches `assets/page_mockups/ShelleyCerny_Website_Services.png`, and confirm all six services render completely with no missing/cut-off content — no dependency on the nav-link work in User Story 2.

### Implementation for User Story 1

- [X] T005 [US1] Create `services.html` at the repository root: copy the `<header class="site-header">...</header>` block verbatim from `index.html` except point this page's own "Services" nav link at `services.html` (itself), copy the `<div class="wave-divider" aria-hidden="true"></div>` block verbatim, then add `<main class="services-main"><div class="services-pattern"><div class="services-card"><h1>Services</h1><div class="services-grid">...</div></div></div></main>` per `contracts/page-contract.md`'s required structure, then copy the `<footer class="site-footer">...</footer>` block verbatim from `index.html`
- [X] T006 [US1] Inside `.services-grid`, add the first `.service-item` block: `<img src="assets/images/ShelleyCerny_UXIcon.png" alt="UX/UI design icon" />`, a subtitle "UX/UI Design", and the description "From wireframes to high fidelity designs, I create digital experiences that are intuitive, intentional, and beautiful." per `data-model.md`'s Service Item #1
- [X] T007 [US1] Add the second `.service-item` block: `assets/images/ShelleyCerny_BrandIcon.png` (alt "Brand identity icon"), subtitle "Brand Identity", description "Logo design, color palettes, typography, and all the pieces that make a brand feel cohesive and memorable." per `data-model.md`'s Service Item #2
- [X] T008 [US1] Add the third `.service-item` block: `assets/images/ShelleyCerny_PrintIcon.png` (alt "Print design icon"), subtitle "Print Design", description "Business cards, letterheads, event materials, and beyond. Designed with the same attention to detail as any digital project." per `data-model.md`'s Service Item #3
- [X] T009 [US1] Add the fourth `.service-item` block: `assets/images/ShelleyCerny_SocialIcon.png` (alt "Social media design icon"), subtitle "Social Media Design", description "On brand, scroll stopping content that actually connects with your audience." per `data-model.md`'s Service Item #4
- [X] T010 [US1] Add the fifth `.service-item` block: `assets/images/ShelleyCerny_WebIcon.png` (alt "Web design icon"), subtitle "Web Design", description "Clean, user centered website designs that look great and feel effortless to navigate." per `data-model.md`'s Service Item #5
- [X] T011 [US1] Add the sixth `.service-item` block: `assets/images/ShelleyCerny_LetteringIcon.png` (alt "Illustration and hand lettering icon"), subtitle "Illustration & Hand Lettering", description "Custom hand lettered signage, murals, and illustrated design elements with a personal touch." per `data-model.md`'s Service Item #6
- [X] T012 [US1] Link `assets/css/styles.css` in `services.html`'s `<head>` (and the same Google Fonts `<link>` tags as `index.html`) so the page renders with the Phase 2 CSS and site typography

**Checkpoint**: `services.html` renders the full "Services" card and all six grid items matching the mockup — User Story 1 is independently testable now (other pages' nav links may still show `#` until Phase 4, which is expected/acceptable for this story's own test)

---

## Phase 4: User Story 2 - Navigate to the Services page from anywhere on the site (Priority: P2)

**Goal**: The "Services" nav link on every existing page leads to `services.html` instead of the `#` placeholder.

**Independent Test**: From `index.html`, `work.html`, `contact.html`, and each `work/<slug>.html` page, click "Services" in the header nav and confirm it lands on `services.html`.

### Implementation for User Story 2

- [X] T013 [US2] Update the "Services" nav link in `index.html` from `href="#"` to `href="services.html"`
- [X] T014 [US2] Update the "Services" nav link in `work.html` from `href="#"` to `href="services.html"`
- [X] T015 [US2] Update the "Services" nav link in `contact.html` from `href="#"` to `href="services.html"`
- [X] T016 [P] [US2] Update the "Services" nav link in `work/the-yoga-space.html` from `href="#"` to `href="../services.html"`
- [X] T017 [P] [US2] Update the "Services" nav link in `work/red-cedar-coffee.html` from `href="#"` to `href="../services.html"`
- [X] T018 [P] [US2] Update the "Services" nav link in `work/bouncy.html` from `href="#"` to `href="../services.html"`
- [X] T019 [P] [US2] Update the "Services" nav link in `work/go-pint.html` from `href="#"` to `href="../services.html"`
- [X] T020 [P] [US2] Update the "Services" nav link in `work/boyd-consulting.html` from `href="#"` to `href="../services.html"`
- [X] T021 [P] [US2] Update the "Services" nav link in `work/invitations.html` from `href="#"` to `href="../services.html"`
- [X] T022 [P] [US2] Update the "Services" nav link in `work/fit4mom.html` from `href="#"` to `href="../services.html"`
- [X] T023 [P] [US2] Update the "Services" nav link in `work/book.html` from `href="#"` to `href="../services.html"`
- [X] T024 [P] [US2] Update the "Services" nav link in `work/wedding-signage.html` from `href="#"` to `href="../services.html"`
- [X] T025 [P] [US2] Update the "Services" nav link in `work/murals.html` from `href="#"` to `href="../services.html"`
- [X] T026 [US2] Cross-check: click "Services" from all 13 pages (T013–T025) and confirm each lands on `services.html` with zero broken links

**Checkpoint**: All 13 existing pages now link to a correct, working Services page — User Story 1 and User Story 2 together are fully functional

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Final validation against the spec's Success Criteria

- [X] T027 [P] Run `quickstart.md` scenario 4 (responsive breakpoints: ~375px, ~768px, ~1440px) against `services.html`; fix any overlapping/cut-off content or grid-reflow issues found in `assets/css/styles.css`
- [X] T028 [P] Run `quickstart.md` scenario 6 (accessibility spot-check): confirm all six icons' `alt` text is non-empty and descriptive
- [X] T029 Run `quickstart.md` scenario 5 (console error check) while clicking through the nav-in path (scenario 1) and loading `services.html` directly, in browser dev tools
- [X] T030 Run `quickstart.md` scenario 3 end-to-end: confirm all six services render completely with correct icon/subtitle/description and no truncation
- [X] T031 Visually diff `services.html` against `assets/page_mockups/ShelleyCerny_Website_Services.png` one more time end-to-end (blob background, card, heading, 3x2 grid, typography) and log/resolve any remaining deviation per spec SC-003

**Checkpoint**: All 6 `quickstart.md` scenarios pass — spec Success Criteria SC-001 through SC-004 are satisfied

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately
- **Foundational (Phase 2)**: Depends on Setup — BLOCKS Phase 3
- **User Story 1 (Phase 3)**: Depends on Phase 2 (needs `.services-card`/`.services-grid`/`.service-item` CSS)
- **User Story 2 (Phase 4)**: Independent of Phase 2/3 CSS work, but T026's cross-check depends on `services.html` existing (Phase 3 complete)
- **Polish (Phase 5)**: Depends on Phases 3 and 4 both being complete

### User Story Dependencies

- **User Story 1 (P1)**: Independently testable after Phase 2 — no dependency on US2
- **User Story 2 (P2)**: Independently authorable at any time (each nav-link edit is a one-line change on an existing file), but its cross-check (T026) needs US1's `services.html` to exist to verify the links actually resolve

### Parallel Opportunities

- T016–T025 (Phase 4) are 10 independent single-line edits across 10 different files — all can run in parallel
- T027, T028 (Phase 5) are independent verification passes and can run in parallel

---

## Parallel Example: User Story 2

```bash
# All 10 detail-page nav-link edits are independent files — launch together:
Task: "Update Services nav link in work/the-yoga-space.html per T016"
Task: "Update Services nav link in work/red-cedar-coffee.html per T017"
Task: "Update Services nav link in work/bouncy.html per T018"
Task: "Update Services nav link in work/go-pint.html per T019"
Task: "Update Services nav link in work/boyd-consulting.html per T020"
Task: "Update Services nav link in work/invitations.html per T021"
Task: "Update Services nav link in work/fit4mom.html per T022"
Task: "Update Services nav link in work/book.html per T023"
Task: "Update Services nav link in work/wedding-signage.html per T024"
Task: "Update Services nav link in work/murals.html per T025"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational
3. Complete Phase 3: User Story 1 (`services.html` renders the full grid, even if other pages' nav links still show `#`)
4. **STOP and VALIDATE**: Visually confirm the page against the mockup
5. Demo if ready — the page alone already delivers "a visitor can see all of Shelley's services"

### Incremental Delivery

1. Setup + Foundational → CSS ready
2. User Story 1 → page renders with all six services → demo the page directly
3. User Story 2 → every existing page's nav link resolves to it → demo full site navigation
4. Polish → full `quickstart.md` pass confirms all Success Criteria

### Suggested Single-Session Order

Given this is a small, single-page feature, the most practical order is
simply T001 → T031 in sequence, parallelizing T016–T025 if convenient,
rather than splitting user stories across separate work sessions.

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- No automated tests were requested for this feature (per spec.md and
  constitution — no build/test framework); validation is manual via
  `quickstart.md`, executed in Phase 5
- Commit after each phase (Setup, Foundational, US1, US2, Polish) per the
  constitution's "commit often at logical checkpoints" workflow rule
- The new page must copy the header/wave-divider/footer markup verbatim
  from `index.html` — do not introduce a templating/include mechanism
  (constitution Principle I: no build step required)
- Per spec Assumptions, no `.service-item` links anywhere (e.g. to Work or
  Contact) — the grid is informational only
