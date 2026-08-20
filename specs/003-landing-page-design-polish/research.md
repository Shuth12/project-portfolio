# Phase 0 Research: Landing Page Design Polish

No technology unknowns exist for this feature (plain CSS/HTML edits to an
already-shipped static page, same stack as `002-landing-page`). The
"unknowns" here are the four designer notes' qualitative magnitudes
("a little more," "a lot more, nothing drastic"). Each is resolved below
with a concrete proposed value, grounded in the current shipped values in
`assets/css/styles.css`, to make Phase 2 tasks actionable. Per the
Constitution's Design Fidelity principle and spec FR-010/SC-001, these
proposed values are a starting point for implementation and MUST be
confirmed against the live rendered result with the designer — this
research does not waive that sign-off step.

## 1. Hero backdrop reveal (Note 1)

- **Decision**: Increase `.hero-visual-backdrop`'s `transform: translate(...)`
  offset from `1.875rem, 1.5625rem` to `2.5rem, 2.1875rem` (a ~33% increase
  on both axes, keeping the existing ~1.2:1 x:y ratio) at the base/desktop
  rule (`styles.css:131`). Scale the two responsive overrides
  (`styles.css:215`, mobile has no explicit backdrop-translate override —
  it relies on the base rule since `.hero-visual` switches to a fixed
  `max-width: 15rem` there) proportionally to the same ~33% increase so the
  reveal remains consistent at every breakpoint.
- **Rationale**: The backdrop is revealed by how far it's translated
  relative to the photo sitting on top of it; increasing the translate
  distance directly and predictably increases the visible sliver of pattern
  without touching the photo, its border-radius, or its shadow. A ~33%
  bump is a visible, deliberate change ("a little more") without being
  large enough to expose the backdrop's edge or unbalance the photo/card
  corner-anchor relationship documented in the existing code comments.
- **Alternatives considered**: Resizing the backdrop image/element itself
  (rejected — changes the backdrop's own scale/pattern density, not just
  its visible margin, and risks distorting the tiled pattern); moving the
  photo instead of the backdrop (rejected — the photo's position also
  anchors the card overlap via `.hero-visual`'s negative margin, so moving
  it would cascade into note 2's spacing change and conflate two edits).

## 2. Main/content/text-block padding, squarer text block, more separation (Note 2)

- **Decision**:
  - `main` padding: increase from `3rem 2rem 4rem` to `4rem 3rem 5rem`
    (`styles.css:92`), scaling the two breakpoint overrides
    (`styles.css:239` mobile, plus the `23.5rem` tightest breakpoint)
    proportionally.
  - `.hero-card` internal padding: increase from `3rem 3rem 3rem 4rem` to
    `4rem 4rem 4rem 5rem` (`styles.css:145`), keeping the left-padding
    delta needed to clear the backdrop's reach (recalculated per note 1's
    new offset), and scale the two responsive overrides accordingly.
  - Squarer text block: reduce the `.hero` grid column ratio from
    `minmax(0, 1fr) minmax(0, 2.84fr)` to `minmax(0, 1fr) minmax(0, 2fr)`
    (`styles.css:99`), narrowing the card column so the same copy wraps
    into more lines and the card reads closer to square; scale the `64rem`
    breakpoint's `2.52fr` companion value down proportionally
    (`styles.css:211`).
  - More separation between card and image/backdrop: reduce the overlap
    magnitude by changing `.hero-visual`'s `margin-right: -1.875rem` to
    `-0.9375rem` (half the current overlap) (`styles.css:109`), and scale
    its `64rem`-breakpoint companion (`styles.css:215`) the same way. This
    keeps the intentional corner-anchor accent (per spec Assumptions) while
    opening up visible space between the two elements, addressing the
    apparent tension with note 1 by keeping the *backdrop reveal* (its own
    translate distance) and the *card/image overlap* (a separate margin
    value) as independently tunable properties.
- **Rationale**: `main` padding and `.hero-card` padding are independent,
  single-property changes with low regression risk. The column-ratio
  change is the most direct way to make the card "take up less space (more
  square)" without touching its padding twice or truncating the bio copy.
  Halving the negative overlap margin is a minimal, reversible way to add
  separation while preserving the designed cascade-and-anchor visual
  language called out in the existing code comments.
- **Alternatives considered**: Setting an explicit `max-width` on
  `.hero-card` instead of changing the grid ratio (rejected — grid ratio
  keeps the existing responsive-scaling approach consistent with the two
  breakpoint overrides already in place, rather than adding a third,
  parallel sizing mechanism); removing the overlap entirely by zeroing the
  negative margin (rejected — spec Assumptions explicitly says the overlap
  accent should be preserved unless the designer says otherwise).

## 3. No em dashes + increased body letter spacing (Note 3)

- **Decision**: Replace both existing em dashes with a comma or restructured
  phrasing:
  - `index.html:6` `<title>Shelley Cerny — Graphic Design Portfolio</title>`
    → `Shelley Cerny, Graphic Design Portfolio`.
  - `index.html:60` "...design brain — the side that obsesses..." → "...
    design brain: the side that obsesses..." (colon reads naturally here
    since the clause that follows explains/elaborates on "both sides").
  - Increase `.hero-card p` (body copy) `letter-spacing` from unset
    (browser default, effectively `normal`/`0`) to `0.01em`
    (`styles.css:158-163`) — a small, modest increase appropriate for
    dense paragraph copy (unlike headings/nav, body text at 1rem/1.6
    line-height gets illegible fast with aggressive tracking).
- **Rationale**: Both em dash replacements preserve the original sentence's
  meaning and rhythm without needing a rewrite. A modest `0.01em` on body
  copy is a standard, safe increment for paragraph text (headings/labels
  in this design already use much larger values like `0.05em`–`0.08em`
  because they're short, uppercase, and set at larger/smaller point sizes
  where wider tracking reads as intentional rather than degrading
  readability).
- **Alternatives considered**: Using a hyphen (`-`) in place of the em dash
  (rejected — reads as a typo/compound-word rather than a clause break);
  leaving body copy letter-spacing at browser default and only bumping
  headings (rejected — spec note 3 explicitly separates "more letter
  spacing" from the nav-specific ask in note 4, implying it targets body
  text elsewhere).

## 4. Nav bar letter spacing (Note 4)

- **Decision**: Increase `.site-nav a` `letter-spacing` from `0.08em` to
  `0.16em` (`styles.css:64`) — double the current value.
- **Rationale**: "A lot more, nothing drastic" calls for a clearly
  perceptible jump rather than a fractional nudge, but nav links are short,
  all-lowercase-with-caps-via-CSS-or-not, single words ("About", "Work",
  "Contact", "Services") in a fixed-width header, so doubling (rather than
  tripling or more) keeps every label on one line at all three existing
  breakpoints without wrapping or crowding the logo, per FR-009's
  no-regression requirement.
- **Alternatives considered**: A larger jump (e.g., `0.24em`+) (rejected as
  first-pass value — risks nav items wrapping or visually crowding the
  centered logo at the `48rem` stacked-nav breakpoint; can be dialed up
  further only if the designer asks for more after reviewing `0.16em`
  live, per FR-010).

## Summary of files touched

- `index.html` — nav link labels unaffected structurally (only CSS
  letter-spacing applies to them); `<title>` and one paragraph sentence
  edited to remove em dashes.
- `assets/css/styles.css` — `.site-nav a`, `.hero`, `.hero-visual`,
  `.hero-visual-backdrop`, `.hero-card`, `.hero-card p`, `main`, and their
  three responsive breakpoint blocks (`64rem`, `48rem`, `23.5rem`).

No new files, dependencies, or NEEDS CLARIFICATION items remain.
