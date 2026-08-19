<!--
Sync Impact Report
- Version change: (unratified template) → 1.0.0 → 1.1.0
- v1.0.0: initial ratification. Added principles:
  - I. Static-Only, No Backend (NON-NEGOTIABLE)
  - II. Design Fidelity
  - III. No Motion or Animation (NON-NEGOTIABLE)
  - IV. CSS-First Interactivity, Minimal JavaScript
  - V. Content Updatable Without Touching Layout
  - VI. Accessibility and Performance Baseline
  Added sections: Explicit Non-Goals, Development Workflow, Governance
- v1.1.0: modified principle III ("No Motion or Animation" →
  "No Site-Implemented Motion or Animation") to add a scoped exception for
  portfolio work samples that are themselves animated deliverables (e.g. a
  client's animated logo GIF), displayed as-provided and never used for site
  chrome/UI. Prompted by an animated asset (assets/images/bouncy/
  Bouncy_Logo_Bounce.gif) that is portfolio content, not a site effect.
- Removed sections: none
- Templates requiring updates: none — dependent templates/commands read this
  constitution at runtime and are out of scope for this command
- Deferred placeholders / TODOs: none — all values derived from docs/PRD.md
  and docs/repo.md
-->

# Shelley Cerny Portfolio Constitution

## Core Principles

### I. Static-Only, No Backend (NON-NEGOTIABLE)
The site MUST remain fully static: hand-authored or templated HTML, CSS, and
(only where genuinely necessary) client-side JavaScript. No server-side code,
backend service, or database MAY be introduced. No build step is required to
publish; if a build or templating step is used to avoid duplicating shared
markup (e.g. nav/footer), its output MUST still be committed or generated as
plain static files that GitHub Pages can serve as-is.
Rationale: the project must stay trivially deployable to GitHub Pages by
either collaborator, with no infrastructure to run or maintain.

### II. Design Fidelity
Implementation MUST closely match the designer-provided mockups: layout,
spacing, color palette, typography, and imagery choices are not to be
reinterpreted. Any point where the web implementation must deviate from the
source design (font licensing, responsive behavior a static mockup doesn't
specify, etc.) MUST be flagged and resolved with the designer before
finalizing — never assumed.
Rationale: the designer owns the visual language; the engineering task is
faithful implementation, not creative reinterpretation.

### III. No Site-Implemented Motion or Animation (NON-NEGOTIABLE)
No animations or motion-based transitions (sliders, parallax, scroll effects,
animated hover/focus states, etc.) MAY be implemented by the site itself,
whether in CSS or JavaScript. Where a source design implies an animated
transition, it MUST be simplified to an instant state change. Simple,
non-animated interactive states (`:hover`, `:focus`, `:active`) implemented
in CSS are permitted.

Exception: a portfolio work sample that is itself an animated deliverable
(e.g. an animated logo GIF created as client work) MAY be displayed as
originally created — the motion is part of the showcased design, not a
site-built effect. Such assets MUST be used as provided (no new animation
authored for the site) and MUST NOT be used for site chrome/UI (navigation,
page transitions, backgrounds).
Rationale: motion effects built into the site are explicitly out of scope
per the PRD, keeping the site's own implementation simple and fast — but the
portfolio must still be able to faithfully show animated work exactly as it
was delivered to a client.

### IV. CSS-First Interactivity, Minimal JavaScript
Primary navigation between pages MUST use standard `<a>` tags so the site is
fully usable with links alone. JavaScript MAY be added only for behavior CSS
genuinely cannot provide (e.g. a mobile nav toggle, image lightbox, portfolio
filtering), and MUST run entirely client-side against static assets — no
animation/motion, no network/server calls. Prefer CSS pseudo-classes for
hover/focus/active states before reaching for JavaScript.
Rationale: keeps the technical footprint minimal and the site resilient;
JavaScript is progressive enhancement, never a dependency for core browsing.

### V. Content Updatable Without Touching Layout
Content additions — new projects, images, copy — MUST be possible without
modifying layout or CSS files. Whatever templating or file structure is
chosen MUST keep content changes confined to content files (e.g. one
page/section per project, or a clearly isolated content area), so either
collaborator can add work without needing front-end skills.
Rationale: the designer needs to add and update portfolio content
independently of the developer.

### VI. Accessibility and Performance Baseline
All images MUST have meaningful `alt` text. Semantic HTML and a logical
heading structure MUST be used throughout. Color contrast MUST be sufficient
within the constraints of the provided design palette. Images MUST be
reasonably optimized/sized for web before committing. Pages MUST show no
console errors and no layout breakage at common breakpoints (mobile and
desktop).
Rationale: baseline for a professional, credible portfolio site that works
for every visitor and loads quickly.

## Explicit Non-Goals

The following are out of scope and MUST NOT be introduced without first
updating `docs/PRD.md` and amending this constitution:

- Blog, CMS, or admin interface for content
- Client-side or server-side contact form (contact is a `mailto:` link only)
- A separate "About" page (bio/intro content lives on the Home/Landing page)
- E-commerce, client login, or password-protected areas
- Analytics/tracking, unless later requested, and then only via a
  lightweight, static-compatible option that requires no backend

## Development Workflow

- All commits MUST follow the Conventional Commits format.
- Each spec/feature MUST be developed on its own branch, branched from
  `development`.
- `development` is the integration branch; `main` is the deployment branch.
  Work MUST NOT be committed directly to `main` outside of a
  `development` → `main` merge.
- For larger groups of tasks within a spec, commit often at logical
  checkpoints rather than as one large commit.
- On completion of a spec, its branch MUST be merged into `development`
  (not directly into `main`).

## Governance

This constitution supersedes ad hoc practices for this repository. Amendments
require: updating this file, incrementing its version per the policy below,
and recording the change in a Sync Impact Report at the top of the file.
Every spec, plan, and implementation MUST be checked against this
constitution; any deviation MUST be explicitly justified in the relevant
spec/plan or resolved by amending the constitution rather than silently
ignored. `docs/PRD.md` and `docs/repo.md` are the source references behind
this constitution's requirements — when they change, this constitution
should be re-synced.

Versioning policy: MAJOR = backward-incompatible removal or redefinition of a
principle or governance rule; MINOR = a new principle added or existing
guidance materially expanded; PATCH = clarifications or wording fixes with no
semantic change.

**Version**: 1.1.0 | **Ratified**: 2026-08-18 | **Last Amended**: 2026-08-18
