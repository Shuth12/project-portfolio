---

description: "Task list template for feature implementation"
---

# Tasks: Landing Page Design Polish

**Input**: Design documents from `/specs/003-landing-page-design-polish/`

**Prerequisites**: [plan.md](./plan.md), [spec.md](./spec.md), [research.md](./research.md), [data-model.md](./data-model.md), [contracts/style-changes.md](./contracts/style-changes.md), [quickstart.md](./quickstart.md)

**Tests**: Not requested in the spec. This feature has no automated test suite in the repo (matches `002-landing-page`); verification is manual visual QA plus designer sign-off, per the Constitution's Design Fidelity principle and spec FR-010/SC-001. Each story below includes a verification task instead of automated test tasks.

**Organization**: Tasks are grouped by user story (from spec.md) to enable independent implementation and validation of each designer note.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3, US4)
- Exact file paths and line references are from `assets/css/styles.css` / `index.html` as of `002-landing-page`; if a prior task in this list shifted line numbers, re-locate the selector by name rather than trusting the stale line number.

## Path Conventions

Single static site project (no `src/`, no frontend/backend split): `index.html` and `assets/css/styles.css` at the repository root, per `plan.md`'s Project Structure. This feature touches only those two files.

---

## Phase 1: Setup

**Purpose**: Establish a working local preview so every later verification task has a consistent baseline.

- [X] T001 Start a local static server from the repo root (`python3 -m http.server 8000`, per [quickstart.md](./quickstart.md#run-the-site-locally)) and confirm the current, pre-change homepage at `http://localhost:8000/index.html` loads correctly at desktop (≥64rem), and the `64rem`, `48rem`, and `23.5rem` breakpoints — this is the "before" baseline every story's verification task will compare against.

---

## Phase 2: Foundational

**Purpose**: Blocking prerequisites shared by all user stories.

None required. This feature only edits two already-shipped files (`index.html`, `assets/css/styles.css`); there is no shared infrastructure, schema, or scaffolding to stand up before story work can begin. Proceed directly to Phase 3 once Phase 1 is complete.

---

## Phase 3: User Story 1 - Hero visual shows more of the patterned underlay (Priority: P1) 🎯 MVP

**Goal**: Increase how much of the patterned backdrop is visibly revealed around the hero photo.

**Independent Test**: Load the homepage and visually compare the exposed margin of the patterned backdrop around the photo against the Phase 1 baseline — a clearly larger sliver of pattern must be visible, with the photo still cleanly aligned on top.

### Implementation for User Story 1

- [X] T002 [US1] In `assets/css/styles.css`, update the `.hero-visual-backdrop` rule's `transform: translate(...)` value from `1.875rem, 1.5625rem` to `2.5rem, 2.1875rem` (around line 131), per [contracts/style-changes.md](./contracts/style-changes.md) item 1.
- [X] T003 [US1] In a local preview (per [quickstart.md](./quickstart.md#1-backdrop-reveal-user-story-1)), confirm the backdrop reveal is visibly larger than the Phase 1 baseline at desktop, and that it still renders cleanly (no clipping outside the rounded corners) at the `64rem` and `48rem` breakpoints; adjust the translate value from T002 if the reveal looks too subtle or too extreme before moving on.

**Checkpoint**: User Story 1 is fully functional and independently verifiable at this point.

---

## Phase 4: User Story 2 - Main content, image, and text block get more breathing room (Priority: P1)

**Goal**: Increase padding around the main content and inside the bio text card, make the bio text card read as more square, and add visible separation between the text card and the image/backdrop behind it.

**Independent Test**: Load the homepage and confirm, without any other pending changes, that (a) outer content padding has visibly increased, (b) the bio card's proportions are closer to square with more internal padding, and (c) there is clearly more separation between the card and the image/backdrop.

### Implementation for User Story 2

- [X] T004 [US2] In `assets/css/styles.css`, update `main`'s `padding` from `3rem 2rem 4rem` to `4rem 3rem 5rem` (around line 92), and its `48rem`-breakpoint override from `2rem 1.25rem 3rem` to `2.5rem 1.75rem 3.5rem` (around line 239), per [contracts/style-changes.md](./contracts/style-changes.md) item 2.
- [X] T005 [US2] In `assets/css/styles.css`, update `.hero-card`'s `padding` at all four rules: base `3rem 3rem 3rem 4rem` → `4rem 4rem 4rem 5rem` (~line 145), `64rem` breakpoint `2rem 2rem 2rem 3.5rem` → `2.75rem 2.75rem 2.75rem 4.25rem` (~line 223), `48rem` breakpoint `5.5rem 1.75rem 1.75rem` → `6rem 2.25rem 2.25rem` (~line 256), and `23.5rem` breakpoint `5rem 1.25rem 1.25rem` → `5.5rem 1.75rem 1.75rem` (~line 274), per [contracts/style-changes.md](./contracts/style-changes.md) item 3.
- [X] T006 [US2] In `assets/css/styles.css`, update `.hero`'s `grid-template-columns` at the base rule from `minmax(0, 1fr) minmax(0, 2.84fr)` to `minmax(0, 1fr) minmax(0, 2fr)` (~line 99), and its `64rem`-breakpoint override from `minmax(0, 1fr) minmax(0, 2.52fr)` to `minmax(0, 1fr) minmax(0, 1.8fr)` (~line 211), per [contracts/style-changes.md](./contracts/style-changes.md) item 4, so the text card column narrows toward a squarer shape.
- [X] T007 [US2] In `assets/css/styles.css`, update `.hero-visual`'s `margin-right` at the base rule from `-1.875rem` to `-0.9375rem` (~line 109), and its `64rem`-breakpoint override from `-1.40625rem` to `-0.703125rem` (~line 215), per [contracts/style-changes.md](./contracts/style-changes.md) item 5, to open up separation from the text card while preserving the corner-overlap accent.
- [X] T008 [US2] In a local preview (per [quickstart.md](./quickstart.md#2-content-padding-squarer-text-block-more-separation-user-story-2)), confirm against the Phase 1 baseline that the hero card reads as more square with visibly more internal/surrounding padding and more separation from the image/backdrop (while the corner-overlap accent is still present), at desktop, `64rem`, `48rem`, and `23.5rem`, with no overlapping content, horizontal scrolling, or cramped/clipped text; adjust T004-T007's values if needed before moving on.

**Checkpoint**: User Stories 1 and 2 both work independently at this point.

---

## Phase 5: User Story 3 - No em dashes and increased letter spacing sitewide (Priority: P2)

**Goal**: Remove every em dash from the site's visible text/metadata and modestly increase body copy letter spacing.

**Independent Test**: Search all visible site text (including `<title>`/meta) for the em dash character and confirm none remain; compare body text letter spacing against the Phase 1 baseline and confirm it has increased.

### Implementation for User Story 3

- [X] T009 [P] [US3] In `index.html`, remove both em dashes: the `<title>` tag (line 6: `Shelley Cerny — Graphic Design Portfolio` → `Shelley Cerny, Graphic Design Portfolio`) and the bio paragraph (line 60: `...design brain — the side that obsesses...` → `...design brain: the side that obsesses...`), per [contracts/style-changes.md](./contracts/style-changes.md) items 8-9.
- [X] T010 [P] [US3] In `assets/css/styles.css`, add `letter-spacing: 0.01em;` to the `.hero-card p` rule (~lines 158-163), per [contracts/style-changes.md](./contracts/style-changes.md) item 6.
- [X] T011 [US3] Run `grep -rn "—" index.html` from the repo root and confirm zero matches; then in a local preview (per [quickstart.md](./quickstart.md#3-no-em-dashes--body-letter-spacing-user-story-3)), confirm both replaced sentences read naturally and the bio paragraph's letter spacing is subtly, legibly increased versus the Phase 1 baseline.

**Checkpoint**: User Stories 1, 2, and 3 all work independently at this point.

---

## Phase 6: User Story 4 - Navigation bar letter spacing increased (Priority: P3)

**Goal**: Noticeably widen nav link letter spacing without it reading as extreme or breaking nav layout.

**Independent Test**: Compare the nav link letter-spacing value against the current baseline (0.08em) — it must be clearly larger while nav items still fit on one line at each breakpoint without wrapping or overlapping the logo.

### Implementation for User Story 4

- [X] T012 [US4] In `assets/css/styles.css`, update `.site-nav a`'s `letter-spacing` from `0.08em` to `0.16em` (~line 64), per [contracts/style-changes.md](./contracts/style-changes.md) item 7.
- [X] T013 [US4] In a local preview (per [quickstart.md](./quickstart.md#4-nav-letter-spacing-user-story-4)), confirm the nav letter spacing is noticeably wider than the Phase 1 baseline but reads as subtle/intentional rather than stretched, and that nav items don't wrap or overlap the logo at the `48rem` stacked-nav breakpoint; adjust T012's value if needed before moving on.

**Checkpoint**: All four user stories are independently functional at this point.

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Confirm the four changes hold up together and get the required design sign-off.

- [X] T014 Run through all four scenarios in [quickstart.md](./quickstart.md#validation-scenarios) together (not one at a time) at desktop, `64rem`, `48rem`, and `23.5rem`, confirming no regressions appear when every change from T002-T013 is combined (per spec FR-009); also complete the [contracts/style-changes.md](./contracts/style-changes.md#verification-checklist) checklist.
- [ ] T015 Share the running local (or deployed) preview with the designer and obtain explicit sign-off that all four notes read as intended, per Constitution Principle II (Design Fidelity) and spec FR-010/SC-001/SC-004. If any value needs adjustment, update [contracts/style-changes.md](./contracts/style-changes.md), re-apply the corresponding CSS/HTML change, and re-run T014 before considering the feature done.

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately.
- **Foundational (Phase 2)**: None — no tasks, nothing blocks the user stories.
- **User Stories (Phase 3-6)**: All depend only on Phase 1 (a working local preview). They do not depend on each other and may be done in any order, though `assets/css/styles.css` is shared across US1/US2/US4, so edits to it should be applied sequentially by whoever is implementing (not literally concurrently) to avoid clobbering each other's changes.
- **Polish (Phase 7)**: Depends on all four user stories (T002-T013) being complete.

### User Story Dependencies

- **User Story 1 (P1)**: Independent — touches only `.hero-visual-backdrop`.
- **User Story 2 (P1)**: Independent — touches `main`, `.hero`, `.hero-visual`, `.hero-card` (different properties than US1's `.hero-visual-backdrop` transform, though in the same section of the file).
- **User Story 3 (P2)**: Independent — touches `index.html` text and `.hero-card p`.
- **User Story 4 (P3)**: Independent — touches only `.site-nav a`.

### Within Each User Story

- CSS/markup edit task(s) before that story's verification task.
- Story's verification task before moving to the next story (or before Phase 7 if all stories are done).

### Parallel Opportunities

- T009 (`index.html`) and T010 (`assets/css/styles.css`) are different files and can be done in parallel.
- Because `assets/css/styles.css` is the shared file for US1, US2, and US4's edit tasks, those tasks are not marked `[P]` relative to each other — apply them one at a time even though the stories themselves are logically independent.
- Phase 1 and Phase 2 have no `[P]` tasks (Phase 1 is a single task; Phase 2 has none).

---

## Parallel Example: User Story 3

```bash
# T009 and T010 touch different files and have no dependency on each other:
Task: "Remove both em dashes in index.html (title tag + bio paragraph)"
Task: "Add letter-spacing: 0.01em to .hero-card p in assets/css/styles.css"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup.
2. Complete Phase 3: User Story 1 (backdrop reveal).
3. **STOP and VALIDATE**: Confirm the backdrop reveal independently via T003.
4. This alone is a shippable, designer-reviewable increment — the smallest of the four notes.

### Incremental Delivery

1. Setup → baseline ready.
2. Add User Story 1 (backdrop reveal) → verify → optionally show designer.
3. Add User Story 2 (padding/proportions/separation) → verify → optionally show designer.
4. Add User Story 3 (em dashes/letter spacing) → verify.
5. Add User Story 4 (nav letter spacing) → verify.
6. Polish: full combined validation (T014) + final designer sign-off (T015).

Given the small size of this feature, doing all four stories in priority order in one pass (rather than shipping each separately) is reasonable — but each story remains independently checkpointed if the designer wants to review incrementally.

---

## Notes

- `[P]` tasks = different files, no dependencies.
- `[Story]` label maps task to its designer note for traceability back to spec.md.
- No automated tests exist for this static site (consistent with `002-landing-page`); verification tasks are manual, browser-based checks against `quickstart.md`.
- Commit after each story's checkpoint (or after each task, per the Constitution's Development Workflow — Conventional Commits, on this feature's branch, targeting `development`).
- Stop at any checkpoint to validate a story independently before continuing.
- Exact rem values in T002-T012 are proposed defaults from `research.md`/`contracts/style-changes.md`; T015's designer sign-off is the actual completion gate per spec FR-010.
