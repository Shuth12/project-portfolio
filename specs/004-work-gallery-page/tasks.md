---

description: "Task list template for feature implementation"
---

# Tasks: Work Gallery Page

**Input**: Design documents from `/specs/004-work-gallery-page/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/page-contract.md, quickstart.md

**Tests**: Not requested for this feature. Validation is manual, via `quickstart.md`'s 7 scenarios (Polish phase runs them).

**Organization**: Tasks are grouped by user story (US1, US2, US3 from spec.md) to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (US1, US2, US3)
- File paths are exact and relative to the repository root unless noted

## Path Conventions

Static multi-page site, no `src/`/`tests/` split — see plan.md's Project
Structure. New files live at `work.html` (repo root) and `work/*.html`;
`assets/css/styles.css` is extended in place. All source images already
exist under `assets/images/<project>/`, per `data-model.md`'s Project
Catalog.

**Note on filenames with spaces**: several existing asset filenames contain
spaces (e.g. `Oh Baby - Baby Shower Invitation.jpg`). When writing `src`/
`href` attributes referencing them, percent-encode spaces as `%20` (e.g.
`Oh%20Baby%20-%20Baby%20Shower%20Invitation.jpg`) rather than leaving raw
spaces in the attribute value.

---

## Phase 1: Setup

**Purpose**: Confirm prerequisites before any page is authored

- [X] T001 Verify every file listed in `specs/004-work-gallery-page/data-model.md`'s Project Catalog table (all 10 projects' `thumbnail` and `detailImages` entries, including `assets/images/flower_baby/Flower Baby Shower Invitation.jpg`) exists on disk under `assets/images/`; note and resolve any mismatch before continuing
- [X] T002 Create the `work/` directory at the repository root (holds the 10 project detail pages created in Phase 4)

**Checkpoint**: All source assets confirmed present; `work/` directory exists

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Shared CSS both User Story 1 and User Story 2 depend on

**⚠️ CRITICAL**: Complete before starting Phase 3 or Phase 4

- [X] T003 [P] Add `.work-main`, `.work-grid`, `.work-tile`, and `.work-tile-title` rules to `assets/css/styles.css`: a `display: grid` gallery (`repeat(5, 1fr)` desktop columns per `research.md`'s Grid layout decision) using the existing `--color-*`/`--font-display` tokens already defined at the top of the file, reflowing at the file's existing `64rem` and `48rem` breakpoints to fewer columns (e.g. 3 then 2/1)
- [X] T004 [P] Add `.project-detail`, `.back-to-work`, and `.project-detail-images` rules to `assets/css/styles.css`: a detail-page layout (heading + back-link + a simple responsive image stack/grid) reusing the same design tokens, with a `:hover`/`:focus-visible` state on `.back-to-work` matching the existing `.site-nav a` treatment (underline, no transition/animation per constitution Principle III)

**Checkpoint**: Shared grid/detail CSS classes exist — User Story 1 and User Story 2 pages can now be authored against them

---

## Phase 3: User Story 1 - Browse the project thumbnail grid (Priority: P1) 🎯 MVP

**Goal**: A visitor loads `work.html` and sees all 10 projects as thumbnails in a grid matching the reference mockup.

**Independent Test**: Load `work.html` directly in a browser and visually confirm all 10 thumbnails render, matching `assets/page_mockups/ShelleyCerny_WebsiteWork.jpg`'s layout/order/palette — no click-through required to pass this story.

### Implementation for User Story 1

- [X] T005 [US1] Create `work.html` at the repository root: copy the `<header class="site-header">...</header>` and `<div class="wave-divider" ...></div>` block verbatim from `index.html`, add `<main class="work-main"><ul class="work-grid">...</ul></main>` containing 10 `<li class="work-tile">` entries in the exact order from `specs/004-work-gallery-page/data-model.md`'s Project Catalog (Yoga Space → Murals), each an `<a href="work/<slug>.html">` wrapping an `<img src="assets/images/<assetFolder>/<thumbnail>" alt="<title> project thumbnail">` and a `<span class="work-tile-title"><title></span>`, per `specs/004-work-gallery-page/contracts/page-contract.md`'s `work.html` structure, then copy the `<footer class="site-footer">...</footer>` block verbatim from `index.html`
- [X] T006 [US1] Link `assets/css/styles.css` in `work.html`'s `<head>` (and the same Google Fonts `<link>` tags as `index.html`) so the grid renders with the Phase 2 CSS and site typography

**Checkpoint**: `work.html` renders all 10 thumbnails matching the mockup — User Story 1 is independently testable now (links may 404 until Phase 4, which is expected/acceptable for this story's own test)

---

## Phase 4: User Story 2 - Open a project's detail page from its thumbnail (Priority: P1)

**Goal**: Clicking any grid thumbnail leads to that project's own detail page showing only that project's images, with a link back to the grid.

**Independent Test**: From `work.html`, click each of the 10 thumbnails in turn and confirm each lands on a distinct page showing only that project's images, with a working "Back to Work" link.

### Implementation for User Story 2

- [X] T007 [P] [US2] Create `work/the-yoga-space.html`: header/wave-divider/footer copied verbatim from `index.html`, `<h1>The Yoga Space</h1>`, `<a class="back-to-work" href="../work.html">` back-link, and a `.project-detail-images` block with `<img>` tags for `../assets/images/yoga_space/YogaSpace_Branding.jpg`, `YogaSpace_Website_Mockup.jpg`, `YogaSpace_Website_Mockup2.jpg` (each with descriptive `alt` text), per `contracts/page-contract.md`
- [X] T008 [P] [US2] Create `work/red-cedar-coffee.html`: same structure, `<h1>Red Cedar Coffee</h1>`, images `../assets/images/red_cedar/RedCedar_MockUp.jpg`, `Red_Cedar_Branding.jpg`
- [X] T009 [P] [US2] Create `work/bouncy.html`: same structure, `<h1>Bouncy</h1>`, images `../assets/images/bouncy/Bouncy_Branding.jpg`, `Bouncy_MockUp.jpg`, and `Bouncy_Logo_Bounce.gif` displayed as-provided per the constitution's portfolio-content motion exception (spec FR-010) — do not use this GIF anywhere else on the site
- [X] T010 [P] [US2] Create `work/go-pint.html`: same structure, `<h1>Go Pint</h1>`, images `../assets/images/go_pints/GoPint_Mockup.jpg`, `GoPints_Branding.jpg`
- [X] T011 [P] [US2] Create `work/boyd-consulting.html`: same structure, `<h1>Boyd Consulting</h1>`, images `../assets/images/boyd/Boyd_Business_Card.jpg`, `Boyd_Letterhead.jpg`, `Boyd_Logo_Ideas.jpg`, `Boyd_PowerPointMockUp.jpg`
- [X] T012 [P] [US2] Create `work/invitations.html`: same structure, `<h1>Invitations</h1>`, images `../assets/images/invitations/Invitation_ShelleyCerny-Invitation.jpg`, `../assets/images/invitations/Oh%20Baby%20-%20Baby%20Shower%20Invitation.jpg`, `../assets/images/invitations/Oil%20Painting%20-%20Wedding%20Invitation.jpg`, and `../assets/images/flower_baby/Flower%20Baby%20Shower%20Invitation.jpg`
- [X] T013 [P] [US2] Create `work/fit4mom.html`: same structure, `<h1>Fit4Mom</h1>`, images `../assets/images/fit_for_mom/Fit4Mom_Email_Mockup.jpg`, `Fit4Mom_Social_Post_Mockup.jpg`, `Fit4Mom_Social_Story_Mockup.jpg`
- [X] T014 [P] [US2] Create `work/book.html`: same structure, `<h1>Book</h1>`, images `../assets/images/book/Book_MockUp_01.jpg`, `Book_MockUp_02.jpg`, `Book_MockUp_03.jpg`
- [X] T015 [P] [US2] Create `work/wedding-signage.html`: same structure, `<h1>Wedding Signage & Stationery</h1>`, images `../assets/images/wedding_sign/Greenery%20-%20Wedding%20Invitation.jpg`, `Minimalist%20Image%20-%20Wedding%20Invitation.jpg`, `WeddingSign_Seating_Chart_01.jpg`, `WeddingSign_Seating_Chart_White.PNG`, `WeddingSign_Social_Media_01.jpg`, `WeddingSign_Table_Numbers_White.jpg`, `WeddingSigns_Cannoli_01.jpg`, `WeddingSigns_Donuts_02.jpg`, `Welcome%20Sign_Katie.jpeg`, `Welcome_Sign_White.PNG`
- [X] T016 [P] [US2] Create `work/murals.html`: same structure, `<h1>Murals</h1>`, images `../assets/images/murals/Murals_Custom%20Art%20CurvedBillboard.jpg`, `Murals_Graffito%20-%20Denim%20Mural%20Mockup.jpg`, `Murals_Lineup%20-%20Lava%20Window%20Sign.jpg`
- [X] T017 [US2] Cross-check every `work.html` grid tile's `href` (from T005) against the 10 filenames created in T007–T016 and confirm each of the 10 slugs matches exactly (fix any mismatch in either `work.html` or the detail page's filename)

**Checkpoint**: All 10 thumbnails now click through to a correct, distinct detail page with a working back-link — User Story 1 and User Story 2 together are fully functional

---

## Phase 5: User Story 3 - Navigate to the Work page from anywhere on the site (Priority: P2)

**Goal**: The site-wide header/footer (logo, nav, footer attribution) is present and functional on `work.html` and every project detail page, consistent with `index.html`.

**Independent Test**: From `index.html`, click "Work" and land on `work.html`; from any `work/<slug>.html` page, confirm the same header/nav/footer as the landing page are present and every nav link still resolves the same way it does on `index.html`.

### Implementation for User Story 3

- [X] T018 [US3] Verify the header (logo linking to `#bio` on `index.html`, "About"/"Work"/"Contact"/"Services" nav) and footer ("Designed by: Shelley Cerny") on `work.html` and all 10 `work/<slug>.html` pages are byte-for-byte consistent with `index.html`'s versions (per `contracts/page-contract.md`); fix any page where the copied markup drifted during Phase 3/4 authoring
- [X] T019 [US3] Click through: `index.html` → "Work" nav → `work.html` → each thumbnail → each detail page's "Back to Work" link → `work.html` → header logo/"About" → `index.html`, confirming every hop lands on the expected page with zero console errors (per quickstart.md scenario 1 and 3)

**Checkpoint**: Header/footer navigation is consistent and functional across the landing page, Work grid, and all 10 detail pages

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Final validation against the spec's Success Criteria

- [X] T020 [P] Run `quickstart.md` scenario 5 (responsive breakpoints: ~375px, ~768px, ~1440px) against `work.html` and at least one `work/<slug>.html` page; fix any overlapping/cut-off content found in `assets/css/styles.css`
- [X] T021 [P] Run `quickstart.md` scenario 6 (keyboard-only navigation) across `work.html` and one detail page; confirm every thumbnail and the back-link are reachable and activatable via Tab/Enter
- [X] T022 [P] Run `quickstart.md` scenario 7 (accessibility spot-check): confirm every `<img>` added in T005 and T007–T016 has non-empty, descriptive `alt` text naming the project and, where useful, the specific piece shown — no empty or generic `alt` values
- [X] T023 Run `quickstart.md` scenario 4 (console error check) while clicking through at least 3 projects' full grid→detail→back path in browser dev tools
- [X] T024 Visually diff `work.html` against `assets/page_mockups/ShelleyCerny_WebsiteWork.jpg` one more time end-to-end (layout, palette, typography, thumbnail order) and log/resolve any remaining deviation per spec SC-005

**Checkpoint**: All 7 `quickstart.md` scenarios pass — spec Success Criteria SC-001 through SC-005 are satisfied

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately
- **Foundational (Phase 2)**: Depends on Setup (needs `work/` to exist for later phases, but T003/T004 themselves only touch `assets/css/styles.css`) — BLOCKS Phases 3 and 4
- **User Story 1 (Phase 3)**: Depends on Phase 2 (needs `.work-grid`/`.work-tile` CSS)
- **User Story 2 (Phase 4)**: Depends on Phase 2 (needs `.project-detail` CSS); T017 additionally depends on T005 (Phase 3) and T007–T016 all being complete
- **User Story 3 (Phase 5)**: Depends on Phase 3 and Phase 4 both being complete (verifies markup created there)
- **Polish (Phase 6)**: Depends on Phases 3, 4, and 5 all being complete

### User Story Dependencies

- **User Story 1 (P1)**: Independently testable after Phase 2 — no dependency on US2/US3
- **User Story 2 (P1)**: Independently testable after Phase 2 (each detail page stands alone); T017's cross-check is the only point of contact with US1's output
- **User Story 3 (P2)**: Verifies US1's and US2's output — not independently buildable before they exist, but is a verification/consistency pass, not new page content

### Parallel Opportunities

- T003 and T004 (Phase 2) touch the same file (`assets/css/styles.css`) but are different, non-overlapping rule blocks — safe to treat as parallel edits if two people coordinate, otherwise do sequentially to avoid a merge conflict in one file
- T007–T016 (Phase 4) are 10 fully independent files — all can be authored in parallel
- T020, T021, T022 (Phase 6) are independent verification passes and can run in parallel

---

## Parallel Example: User Story 2

```bash
# All 10 project detail pages are independent files — launch together:
Task: "Create work/the-yoga-space.html per T007"
Task: "Create work/red-cedar-coffee.html per T008"
Task: "Create work/bouncy.html per T009"
Task: "Create work/go-pint.html per T010"
Task: "Create work/boyd-consulting.html per T011"
Task: "Create work/invitations.html per T012"
Task: "Create work/fit4mom.html per T013"
Task: "Create work/book.html per T014"
Task: "Create work/wedding-signage.html per T015"
Task: "Create work/murals.html per T016"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational
3. Complete Phase 3: User Story 1 (`work.html` grid renders correctly, even if links 404)
4. **STOP and VALIDATE**: Visually confirm the grid against the mockup
5. Demo if ready — the grid alone already delivers "see all my work at a glance"

### Incremental Delivery

1. Setup + Foundational → CSS and folder ready
2. User Story 1 → grid renders → demo the visual gallery
3. User Story 2 → every thumbnail click-through works → demo full navigation
4. User Story 3 → header/footer consistency verified across every new page
5. Polish → full `quickstart.md` pass confirms all Success Criteria

### Suggested Single-Session Order

Given this is a small, tightly-coupled static-content feature (one grid page
+ 10 near-identical detail pages), the most practical order is simply
T001 → T024 in sequence, parallelizing T007–T016 if multiple
files-at-once authoring is convenient, rather than splitting user stories
across separate work sessions.

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- No automated tests were requested for this feature (per spec.md and
  constitution — no build/test framework); validation is manual via
  `quickstart.md`, executed in Phase 6
- Commit after each phase (Setup, Foundational, US1, US2, US3, Polish) per
  the constitution's "commit often at logical checkpoints" workflow rule
- Every new page must copy the header/wave-divider/footer markup verbatim
  from `index.html` — do not introduce a templating/include mechanism
  (constitution Principle I: no build step required)
