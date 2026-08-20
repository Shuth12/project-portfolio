# Quickstart: Validating the Landing Page Design Polish

## Prerequisites

- This is a static site with no build step. Any static file server works.
- No dependencies to install.

## Run the site locally

From the repo root:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/index.html` in a browser. (Opening
`index.html` directly via `file://` also works for this feature, since no
server-side behavior is involved.)

## Validation scenarios

Each scenario maps to an acceptance scenario in
[`spec.md`](./spec.md#user-scenarios--testing) and the checklist in
[`contracts/style-changes.md`](./contracts/style-changes.md#verification-checklist).

### 1. Backdrop reveal (User Story 1)

1. Load the homepage at desktop width (≥ `64rem`).
2. Confirm a visibly wider margin of the patterned backdrop is exposed
   around the profile photo compared to the pre-change screenshot/commit
   (`a40eee1`).
3. Resize the browser through the `64rem` and `48rem` breakpoints; confirm
   the reveal scales down proportionally and never clips outside the hero
   visual's rounded corners.

### 2. Content padding, squarer text block, more separation (User Story 2)

1. At desktop width, confirm the outer padding around the hero section
   (between content and header/page edges) is visibly larger.
2. Confirm the bio text card reads as narrower/more square relative to its
   height than before, and its internal padding around the heading,
   paragraph, and button is visibly larger.
3. Confirm there is more visible separation between the text card and the
   image/backdrop behind it, while the corner-overlap accent is still
   present (the card doesn't fully detach from the image group).
4. Resize through `64rem`, `48rem`, and `23.5rem`; confirm no overlapping
   content, no horizontal scrollbar, and the bio paragraph still reads
   comfortably (no cramped or clipped text).

### 3. No em dashes + body letter spacing (User Story 3)

1. Run `grep -rn "—" index.html` from the repo root — expect no output
   (zero matches) in visible text/metadata. (A match inside a CSS comment
   in `assets/css/styles.css`, e.g. the "renders undistorted" note, is
   source-code-only and out of scope — it never renders on the page.)
2. View page source or inspect the `<title>` tag in the browser tab —
   confirm it reads "Shelley Cerny, Graphic Design Portfolio" (or
   equivalent, no em dash).
3. Read the bio paragraph and confirm the previously em-dash-joined clause
   now reads naturally with the replacement punctuation.
4. Visually compare the bio paragraph's letter spacing to the pre-change
   version — confirm a subtle, modest increase that doesn't hurt
   readability.

### 4. Nav letter spacing (User Story 4)

1. At desktop width, confirm the nav link labels ("About", "Work",
   "Contact", "Services") have noticeably more open letter spacing than
   the pre-change baseline, without looking stretched/broken.
2. Resize to the `48rem` breakpoint where the nav stacks/centers under the
   logo; confirm no nav item wraps onto two lines or overlaps another
   element.

## Sign-off

Per Constitution Principle II (Design Fidelity) and spec FR-010/SC-001:
share the running local preview (or a deployed preview) with the designer
and get explicit confirmation that all four notes read as intended before
merging. If any value needs adjustment, update
[`contracts/style-changes.md`](./contracts/style-changes.md) and the
corresponding CSS, then re-run the scenarios above.
