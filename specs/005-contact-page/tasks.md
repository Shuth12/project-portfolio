---

description: "Task list template for feature implementation"
---

# Tasks: Contact Page

**Input**: Design documents from `/specs/005-contact-page/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/page-contract.md, quickstart.md

**Tests**: Not requested for this feature. Validation is manual, via `quickstart.md`'s 7 scenarios (Polish phase runs them).

**Organization**: Tasks are grouped by user story (US1, US2 from spec.md) to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (US1, US2)
- File paths are exact and relative to the repository root unless noted

## Path Conventions

Static multi-page site, no `src/`/`tests/` split — see plan.md's Project
Structure. The new file lives at `contact.html` (repo root);
`assets/css/styles.css` is extended in place. All source images already
exist under `assets/images/`.

**Note on relative paths**: root-level pages (`index.html`, `work.html`)
link to the new page as `contact.html`; pages under `work/` link to it as
`../contact.html`, matching the existing relative-path convention used for
`work.html`/`index.html#bio` links on those pages.

---

## Phase 1: Setup

**Purpose**: Confirm prerequisites before the page is authored

- [X] T001 Verify `assets/images/Shelleycerny-checkared.png` and `assets/images/ShelleyCerny_Photo02.png` exist on disk; note and resolve any mismatch before continuing

**Checkpoint**: All source assets confirmed present

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Shared CSS that User Story 1's page depends on

**⚠️ CRITICAL**: Complete before starting Phase 3

- [X] T002 Add `.contact-main`, `.contact-card`, `.contact-card-content`, and `.contact-photo` rules to `assets/css/styles.css`: `.contact-main` gets a tiled checkerboard background using `Shelleycerny-checkared.png` (per `research.md`'s background-pattern decision — one tile repetition's width matching the existing `75rem` card max-width already used by `.work-grid`/`.project-detail`); `.contact-card` is an off-white, rounded, drop-shadowed card (reuse `--color-background`, a `border-radius` consistent with `.hero-card`, and a new `box-shadow` value); `.contact-photo` overlaps the card's right edge with its own `box-shadow`, reusing the `.hero-photo`/`.hero-card` overlap technique per `research.md`; reflow the card/photo stacking at the file's existing `64rem`, `48rem`, and `23.5rem` breakpoints so nothing overlaps or gets cut off narrower

**Checkpoint**: Shared contact-page CSS classes exist — User Story 1 can now be authored against them

---

## Phase 3: User Story 1 - Reach out via email from the Contact page (Priority: P1) 🎯 MVP

**Goal**: A visitor loads `contact.html` and can click "Send Me An Email" to open a pre-addressed email draft.

**Independent Test**: Load `contact.html` directly in a browser, visually confirm it matches `assets/page_mockups/ShelleyCerny_Website_Contact.png`, and click "Send Me An Email" to confirm it opens a mail client addressed to shelley.cerny@gmail.com — no dependency on the nav-link work in User Story 2.

### Implementation for User Story 1

- [X] T003 [US1] Create `contact.html` at the repository root: copy the `<header class="site-header">...</header>` block verbatim from `index.html` except point this page's own "Contact" nav link at `contact.html` (itself), copy the `<div class="wave-divider" aria-hidden="true"></div>` block verbatim, then add `<main class="contact-main"><div class="contact-card"><div class="contact-card-content">...</div><img class="contact-photo" .../></div></main>` per `contracts/page-contract.md`'s required structure, then copy the `<footer class="site-footer">...</footer>` block verbatim from `index.html`
- [X] T004 [US1] Inside `.contact-card-content`, add `<h1>Say Hello!</h1>` styled like `index.html`'s `.hero-card h1` (reuse that class or an equivalent selector per `data-model.md`), the body paragraph from `contracts/page-contract.md` (the exact copy from spec.md's Input), and `<a class="button button--resume" href="mailto:shelley.cerny@gmail.com">Send Me An Email</a>`
- [X] T005 [US1] Add `<img class="contact-photo" src="assets/images/ShelleyCerny_Photo02.png" alt="Shelley Cerny smiling, sitting on a couch" />` inside `.contact-card`, positioned overlapping the card's right edge per the Phase 2 CSS
- [X] T006 [US1] Link `assets/css/styles.css` in `contact.html`'s `<head>` (and the same Google Fonts `<link>` tags as `index.html`) so the page renders with the Phase 2 CSS and site typography

**Checkpoint**: `contact.html` renders the full card/photo/CTA matching the mockup and the mailto button works — User Story 1 is independently testable now (other pages' nav links may still show `#` until Phase 4, which is expected/acceptable for this story's own test)

---

## Phase 4: User Story 2 - Navigate to the Contact page from anywhere on the site (Priority: P2)

**Goal**: The "Contact" nav link on every existing page leads to `contact.html` instead of the `#` placeholder.

**Independent Test**: From `index.html`, `work.html`, and each `work/<slug>.html` page, click "Contact" in the header nav and confirm it lands on `contact.html`.

### Implementation for User Story 2

- [X] T007 [US2] Update the "Contact" nav link in `index.html` from `href="#"` to `href="contact.html"`
- [X] T008 [US2] Update the "Contact" nav link in `work.html` from `href="#"` to `href="contact.html"`
- [X] T009 [P] [US2] Update the "Contact" nav link in `work/the-yoga-space.html` from `href="#"` to `href="../contact.html"`
- [X] T010 [P] [US2] Update the "Contact" nav link in `work/red-cedar-coffee.html` from `href="#"` to `href="../contact.html"`
- [X] T011 [P] [US2] Update the "Contact" nav link in `work/bouncy.html` from `href="#"` to `href="../contact.html"`
- [X] T012 [P] [US2] Update the "Contact" nav link in `work/go-pint.html` from `href="#"` to `href="../contact.html"`
- [X] T013 [P] [US2] Update the "Contact" nav link in `work/boyd-consulting.html` from `href="#"` to `href="../contact.html"`
- [X] T014 [P] [US2] Update the "Contact" nav link in `work/invitations.html` from `href="#"` to `href="../contact.html"`
- [X] T015 [P] [US2] Update the "Contact" nav link in `work/fit4mom.html` from `href="#"` to `href="../contact.html"`
- [X] T016 [P] [US2] Update the "Contact" nav link in `work/book.html` from `href="#"` to `href="../contact.html"`
- [X] T017 [P] [US2] Update the "Contact" nav link in `work/wedding-signage.html` from `href="#"` to `href="../contact.html"`
- [X] T018 [P] [US2] Update the "Contact" nav link in `work/murals.html` from `href="#"` to `href="../contact.html"`
- [X] T019 [US2] Cross-check: click "Contact" from all 12 pages (T007–T018) and confirm each lands on `contact.html` with zero broken links

**Checkpoint**: All 12 existing pages now link to a correct, working Contact page — User Story 1 and User Story 2 together are fully functional

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Final validation against the spec's Success Criteria

- [X] T020 [P] Run `quickstart.md` scenario 4 (responsive breakpoints: ~375px, ~768px, ~1440px) against `contact.html`; fix any overlapping/cut-off content found in `assets/css/styles.css`
- [X] T021 [P] Run `quickstart.md` scenario 5 (keyboard-only navigation): confirm the "Send Me An Email" button is reachable and activatable via Tab/Enter
- [X] T022 [P] Run `quickstart.md` scenario 7 (accessibility spot-check): confirm the photo's `alt` text is non-empty and descriptive
- [X] T023 Run `quickstart.md` scenario 6 (console error check) while clicking through the nav-in path (scenario 1) and the mailto CTA (scenario 3) in browser dev tools
- [X] T024 Run `quickstart.md` scenario 3 end-to-end: click "Send Me An Email" and confirm a mail client opens pre-addressed to shelley.cerny@gmail.com
- [X] T025 Visually diff `contact.html` against `assets/page_mockups/ShelleyCerny_Website_Contact.png` one more time end-to-end (checkerboard background, card, photo overlap, typography, button) and log/resolve any remaining deviation per spec SC-004

**Checkpoint**: All 7 `quickstart.md` scenarios pass — spec Success Criteria SC-001 through SC-005 are satisfied

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately
- **Foundational (Phase 2)**: Depends on Setup — BLOCKS Phase 3
- **User Story 1 (Phase 3)**: Depends on Phase 2 (needs `.contact-card`/`.contact-photo` CSS)
- **User Story 2 (Phase 4)**: Independent of Phase 2/3 CSS work, but T019's cross-check depends on `contact.html` existing (Phase 3 complete)
- **Polish (Phase 5)**: Depends on Phases 3 and 4 both being complete

### User Story Dependencies

- **User Story 1 (P1)**: Independently testable after Phase 2 — no dependency on US2
- **User Story 2 (P2)**: Independently authorable at any time (each nav-link edit is a one-line change on an existing file), but its cross-check (T019) needs US1's `contact.html` to exist to verify the links actually resolve

### Parallel Opportunities

- T009–T018 (Phase 4) are 10 independent single-line edits across 10 different files — all can run in parallel
- T020, T021, T022 (Phase 5) are independent verification passes and can run in parallel

---

## Parallel Example: User Story 2

```bash
# All 10 detail-page nav-link edits are independent files — launch together:
Task: "Update Contact nav link in work/the-yoga-space.html per T009"
Task: "Update Contact nav link in work/red-cedar-coffee.html per T010"
Task: "Update Contact nav link in work/bouncy.html per T011"
Task: "Update Contact nav link in work/go-pint.html per T012"
Task: "Update Contact nav link in work/boyd-consulting.html per T013"
Task: "Update Contact nav link in work/invitations.html per T014"
Task: "Update Contact nav link in work/fit4mom.html per T015"
Task: "Update Contact nav link in work/book.html per T016"
Task: "Update Contact nav link in work/wedding-signage.html per T017"
Task: "Update Contact nav link in work/murals.html per T018"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational
3. Complete Phase 3: User Story 1 (`contact.html` renders and the mailto button works, even if other pages' nav links still show `#`)
4. **STOP and VALIDATE**: Visually confirm the page against the mockup and click the CTA
5. Demo if ready — the page alone already delivers "a visitor can email Shelley"

### Incremental Delivery

1. Setup + Foundational → CSS ready
2. User Story 1 → page renders and CTA works → demo the page directly
3. User Story 2 → every existing page's nav link resolves to it → demo full site navigation
4. Polish → full `quickstart.md` pass confirms all Success Criteria

### Suggested Single-Session Order

Given this is a small, single-page feature, the most practical order is
simply T001 → T025 in sequence, parallelizing T009–T018 if convenient,
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
