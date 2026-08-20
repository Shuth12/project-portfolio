# Contract: Style & Content Changes

This is the interface contract for this feature: the exact, current →
proposed values each implementation task must apply. Selectors/lines refer
to `assets/css/styles.css` and `index.html` as of `002-landing-page`. Exact
values are proposed defaults from [`research.md`](../research.md) — the
Design Fidelity gate (spec FR-010 / SC-001) requires designer confirmation
of the rendered result; if the designer asks for a different amount, update
this table and re-derive tasks from it rather than improvising in code.

## CSS changes — `assets/css/styles.css`

| # | Selector | Property | Current | Proposed | Note |
|---|---|---|---|---|---|
| 1 | `.hero-visual-backdrop` (base) | `transform: translate(...)` | `1.875rem, 1.5625rem` | `2.5rem, 2.1875rem` | Backdrop reveal (Note 1) |
| 1 | `.hero-visual-backdrop` (implied at `64rem` via `.hero-visual` scaling — see #5) | — | — | — | Scales with #5's ratio |
| 2 | `main` (base) | `padding` | `3rem 2rem 4rem` | `4rem 3rem 5rem` | Content padding (Note 2) |
| 2 | `main` (`48rem` breakpoint) | `padding` | `2rem 1.25rem 3rem` | `2.5rem 1.75rem 3.5rem` | Scaled proportionally |
| 3 | `.hero-card` (base) | `padding` | `3rem 3rem 3rem 4rem` | `4rem 4rem 4rem 5rem` | Card internal padding (Note 2); left value must still clear backdrop reach per existing code comment — recompute against #1/#5's new offsets |
| 3 | `.hero-card` (`64rem` breakpoint) | `padding` | `2rem 2rem 2rem 3.5rem` | `2.75rem 2.75rem 2.75rem 4.25rem` | Scaled proportionally |
| 3 | `.hero-card` (`48rem` breakpoint) | `padding` | `5.5rem 1.75rem 1.75rem` | `6rem 2.25rem 2.25rem` | Scaled proportionally |
| 3 | `.hero-card` (`23.5rem` breakpoint) | `padding` | `5rem 1.25rem 1.25rem` | `5.5rem 1.75rem 1.75rem` | Scaled proportionally |
| 4 | `.hero` (base) | `grid-template-columns` | `minmax(0, 1fr) minmax(0, 2.84fr)` | `minmax(0, 1fr) minmax(0, 2fr)` | Squarer text block (Note 2) |
| 4 | `.hero` (`64rem` breakpoint) | `grid-template-columns` | `minmax(0, 1fr) minmax(0, 2.52fr)` | `minmax(0, 1fr) minmax(0, 1.8fr)` | Scaled proportionally |
| 5 | `.hero-visual` (base) | `margin-right` | `-1.875rem` | `-0.9375rem` | More separation from card, keep overlap accent (Note 2) |
| 5 | `.hero-visual` (`64rem` breakpoint) | `margin-right` | `-1.40625rem` | `-0.703125rem` | Scaled proportionally |
| 6 | `.hero-card p` | `letter-spacing` | *(unset)* | `0.01em` | Body copy letter spacing (Note 3) |
| 7 | `.site-nav a` | `letter-spacing` | `0.08em` | `0.16em` | Nav letter spacing (Note 4) |

## Markup/content changes — `index.html`

| # | Location | Current | Proposed |
|---|---|---|---|
| 8 | `<title>` (line 6) | `Shelley Cerny — Graphic Design Portfolio` | `Shelley Cerny, Graphic Design Portfolio` |
| 9 | Bio paragraph (line 60) | `...design brain — the side that obsesses...` | `...design brain: the side that obsesses...` |

## Verification checklist (maps to spec Success Criteria)

- [X] `grep -rn "—" index.html` (and any other future page) returns no
      matches in visible text/metadata → SC-002
- [X] Homepage visually reviewed at desktop, `64rem`, `48rem`, and `23.5rem`
      breakpoints with no overlap, horizontal scroll, or wrapping
      regressions → SC-003
- [ ] Designer reviews the live rendered page against all four notes and
      signs off → SC-001, SC-004
