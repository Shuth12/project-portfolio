---

description: "Task list template for feature implementation"
---

# Tasks: Landing Page (Home / About)

**Input**: Design documents from `/specs/002-landing-page/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/page-structure.md, quickstart.md

**Tests**: Not included — per `plan.md`'s Testing decision (consistent with `001-scaffold-site-deploy`), this is a single static content page with no automated test framework; verification is manual via `quickstart.md`, referenced directly in the validation tasks below.

**Organization**: Tasks are grouped by user story (spec.md) to enable independent implementation and testing of each story. Nearly all tasks touch the same two files (`index.html`, `assets/css/styles.css`), so `[P]` is used sparingly — only where tasks genuinely touch separate files.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

Single static site at the repository root (per `plan.md`'s Structure Decision): `index.html` and `assets/css/styles.css`, no `src/`, no build step.

---

## Phase 1: Setup

**Purpose**: Wire up the shared design-system inputs (fonts, color/font tokens) that every user story's markup and styles depend on.

- [X] T001 In `index.html` `<head>`, add the Google Fonts CDN `<link>` tags for Space Mono (weight 700) and Inter (weights 400/500) per `research.md`'s Typography decision, and replace the placeholder `<title>` with "Shelley Cerny — Graphic Design Portfolio" plus a short `<meta name="description">`. (Revised from an initial Baloo 2 pick after visual comparison against the mockup showed a monospaced, not rounded, display face.)
- [X] T002 [P] In `assets/css/styles.css`, add a `:root` block defining the CSS custom properties from `contracts/page-structure.md`'s Shared design tokens contract (`--color-background: #F9F8F3`, `--color-panel-teal: #1F7A8C`, `--color-accent-yellow: #E8B601`, `--color-text-green: #5D8C6A`, `--color-text-body: #0C0B09`, `--color-cta-purple: #9C8BBF`, `--color-text-on-dark: #FFFFFF`, plus `--font-display: "Space Mono", monospace` and `--font-body: "Inter", sans-serif`), replacing the existing placeholder color/font declarations.

**Checkpoint**: Design tokens and fonts are loaded and available to every subsequent task.

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Build the page skeleton, header shell, and footer that every user story's content sits inside. Nav links remain inert (`href="#"`) here — wiring real destinations is User Story 3's job.

**⚠️ CRITICAL**: No user story work can begin until this phase is complete.

- [X] T003 In `index.html`, replace the placeholder `<body>` (currently just an `<h1>`/`<p>` in `<main>`) with the page skeleton: `<header>`, `<main>`, and `<footer>` landmark elements, using semantic HTML per constitution Principle VI.
- [X] T004 In `index.html`'s `<header>`, add the logo `<img>` (placeholder `src="assets/images/logo/ShelleyCerny-Logo.svg"`, descriptive `alt="Shelley Cerny"`) and a `<nav>` containing four `<a>` links labeled About, Work, Contact, Services (in that order per the mockup), each with an inert `href="#"` for now.
- [X] T005 In `assets/css/styles.css`, style the header/nav: cream background using `--color-background`, logo sizing, nav laid out with flexbox using `--font-display` and `--color-text-green`, and a `flex-wrap` responsive rule so the nav wraps/stacks cleanly at narrow widths with no JavaScript (constitution Principle IV; depends on T003, T004).
- [X] T006 In `index.html`'s `<footer>`, add the attribution text "Designed by: Shelley Cerny" (depends on T003).
- [X] T007 In `assets/css/styles.css`, style the footer: mustard-yellow band using `--color-accent-yellow`, white text using `--color-text-on-dark` and `--font-display`, matching the mockup exactly per the spec's design-fidelity-over-contrast clarification (depends on T006).

**Checkpoint**: Page loads with a styled header (logo + inert nav) and footer; foundation ready for user story work.

---

## Phase 3: User Story 1 - Learn who Shelley is (Priority: P1) 🎯 MVP

**Goal**: A visitor sees Shelley's photo, name, and full biography immediately on page load, without clicking anything.

**Independent Test**: Load `index.html` in a browser and confirm a visitor can read Shelley's name, tagline/role, and biography without clicking anything, at both desktop and mobile widths.

### Implementation for User Story 1

- [X] T008 [US1] In `index.html`'s `<main>`, add the hero/bio section: a headshot `<img>` (placeholder `src="assets/images/profile/ShelleyCerny-Headshot.jpg"`, descriptive `alt="Shelley Cerny"`), an `id="bio"` anchor target on the section, the `<h1>` heading "Hi I'm Shelley,", and the biography paragraph (background, design focus, and the role she's seeking) matching the tone and content of `ShelleyCerny_WebsiteAbout.jpg` (spec FR-002, FR-003).
- [X] T009 [US1] In `assets/css/styles.css`, style the hero/bio section: the two-column composition (photo on a teal panel using `--color-panel-teal` and mustard accent shape using `--color-accent-yellow` on one side, a cream bio card using `--color-background` and `--color-text-body`/`--font-body` on the other), matching the mockup's layout, spacing, and colors (depends on T008).
- [X] T010 [US1] In `assets/css/styles.css`, add responsive rules so the hero/bio section reflows without overlapping or cut-off content at ~375px, ~768px, and ~1440px viewport widths (spec SC-003; depends on T009).
- [X] T011 [US1] Run `quickstart.md` steps 1–2 (page loads with real content; visual comparison against `ShelleyCerny_WebsiteAbout.jpg`) and confirm no console errors and no layout breakage.

**Checkpoint**: User Story 1 is fully functional and independently testable — page loads with header, styled bio content, and footer.

---

## Phase 4: User Story 2 - Download Shelley's resume (Priority: P2)

**Goal**: A visitor can click "Download My Resume" to open/download the resume file.

**Independent Test**: Click the "Download My Resume" button and confirm it attempts to open/download a resume file (a placeholder path, per the spec's resolved clarification, until the real PDF is supplied).

### Implementation for User Story 2

- [X] T012 [US2] In `index.html`'s hero/bio section, add the "Download My Resume" CTA `<a>` styled as a button, linking to the placeholder path `assets/resume/ShelleyCerny-Resume.pdf` (spec FR-004, FR-013).
- [X] T013 [US2] In `assets/css/styles.css`, style the CTA button: rounded shape, `--color-cta-purple` background, `--color-text-on-dark` text, `--font-display`, with a CSS-only `:hover`/`:focus` state (instant, no transition, per constitution Principle III; depends on T012).
- [X] T014 [US2] Run `quickstart.md` step 3's resume-button check and confirm clicking the button attempts to load the placeholder path with no JavaScript console errors (spec SC-002).

**Checkpoint**: User Stories 1 and 2 both work independently — bio content renders and the resume CTA is wired to its placeholder destination.

---

## Phase 5: User Story 3 - Navigate to other parts of the site (Priority: P3)

**Goal**: A visitor can use the header nav to jump to the bio section or reach placeholder destinations for Work, Contact, and Services.

**Independent Test**: Click each header navigation link (About, Work, Contact, Services) and confirm each resolves to its agreed destination (an in-page anchor or a placeholder page) with no broken link or console error.

### Implementation for User Story 3

- [X] T015 [US3] In `index.html`, update the nav `<a>` hrefs from the Foundational phase's inert `"#"` placeholders to their real targets: About → `#bio`, Work → `work.html`, Services → `#` (or `services.html`), Contact → `#` (spec FR-010–FR-012, FR-014).
- [X] T016 [US3] In `assets/css/styles.css`, add `scroll-margin-top` (or equivalent) to the `#bio` section so the in-page "About" anchor doesn't land content underneath the header (depends on T015).
- [X] T017 [US3] Run `quickstart.md` step 3's remaining checks (About scrolls to bio; Work/Services/Contact resolve to their placeholder destinations) and confirm no console errors even though several destinations are expected 404s (spec SC-002).

**Checkpoint**: All three user stories are independently functional — full page content, working resume CTA, and working nav.

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Final verification across all user stories against the spec's remaining success criteria and constitution gates.

- [X] T018 [P] Audit every `<img>` in `index.html` (logo, headshot) for descriptive, non-redundant `alt` text per spec FR-008.
- [X] T019 Run `quickstart.md` step 6 (disable JavaScript, reload) and confirm all content and nav links still render and function with no JavaScript at all (constitution Principle IV).
- [X] T020 Run `quickstart.md` step 5 (accessibility baseline: alt text, heading structure) end-to-end, and confirm the two documented contrast exceptions (footer white-on-mustard, nav green-on-cream — see `research.md` and `plan.md`'s Complexity Tracking) are present exactly as designed, not accidental additional low-contrast text elsewhere on the page.
- [X] T021 Do a final full run of `quickstart.md` (all 6 steps) end-to-end as the release check for this feature.

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — can start immediately.
- **Foundational (Phase 2)**: Depends on Setup completion — BLOCKS all user stories.
- **User Stories (Phase 3–5)**: All depend on Foundational phase completion. Because all stories edit the same two files, they are listed in priority order (P1 → P2 → P3) for a single implementer; a team could still work them in parallel with care around merge conflicts.
- **Polish (Phase 6)**: Depends on all three user stories being complete.

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) — no dependency on other stories.
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) — adds the CTA button independently of US1's bio copy; not blocked by US1.
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) — only rewires nav `href`s already scaffolded in Foundational; not blocked by US1 or US2, though T015's `#bio` target assumes T008 (US1) has added that `id`.

### Within Each User Story

- Markup task before styling task (styling selectors target markup added first).
- Styling task before the story's `quickstart.md` validation task.

### Parallel Opportunities

- T001 and T002 can run in parallel (different files: `index.html` vs. `assets/css/styles.css`).
- Because almost every other task edits `index.html` and/or `assets/css/styles.css`, most tasks are sequential to avoid same-file conflicts, even across different user stories.
- T018 (alt-text audit) can run in parallel with T019/T020 preparation, since it's a read/verify pass on already-completed markup rather than new styling work.

---

## Parallel Example: Setup Phase

```bash
# Launch both Setup tasks together (different files):
Task: "Add Google Fonts links and update <title>/meta description in index.html"
Task: "Add CSS custom properties (color/font tokens) in assets/css/styles.css"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL — blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Run `quickstart.md` steps 1–2 against User Story 1 alone
5. This is a deployable MVP: header, footer, and full bio content, even before the resume CTA or nav links are wired

### Incremental Delivery

1. Complete Setup + Foundational → header/footer shell ready
2. Add User Story 1 → validate → this is the MVP (bio content readable)
3. Add User Story 2 → validate → resume CTA wired to its placeholder
4. Add User Story 3 → validate → nav fully wired
5. Complete Phase 6 Polish → final `quickstart.md` release check

---

## Notes

- `[P]` tasks = different files, no dependencies.
- `[Story]` label maps task to specific user story for traceability.
- No automated tests are generated for this feature (see Tests note above); `quickstart.md` steps stand in for test tasks.
- Commit after each task or logical group, per `docs/repo.md`'s conventional-commits and "commit often" guidance.
- Headshot, logo, and resume files remain placeholders throughout this task list per the spec's resolved clarifications — do not fabricate placeholder binary files; reference the paths only.
