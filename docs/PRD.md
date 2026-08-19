# Product Requirements Document: Shelley Cernys— Graphic Design Portfolio Website

**Author:** Rick
**Status:** Approved
**Last updated:** August 18, 2026

## 1. Overview

A personal portfolio website for a graphic designer to showcase her work, make it easy for potential clients or employers to view her design projects, and provide a simple way to get in touch. The site will be built primarily with HTML and CSS. JavaScript may be introduced if a feature genuinely calls for it, but the hard constraint is that the site remains fully static — no backend, no server-side processing — and is directly hostable on GitHub Pages. Animations/motion effects remain out of scope. The site will closely follow an existing set of designs/mockups rather than introduce new design decisions.

## 2. Goals

- Present a curated, professional showcase of her graphic design work.
- Make it trivially easy for a visitor to browse projects and get in touch by email.
- Faithfully implement the provided designs in code, with minimal deviation.
- Keep the technical footprint minimal: a static site (HTML/CSS, with JavaScript added only where genuinely needed) deployable directly to GitHub Pages, ideally with no build pipeline required.
- Keep the codebase simple enough that either of us can update content (new projects, images, copy) without needing to touch layout/CSS.

## 3. Non-Goals

- No animations or motion-based transitions (sliders, parallax, scroll effects, etc.) — this applies regardless of whether JavaScript is used elsewhere on the site.
- No backend, server, or database of any kind — JavaScript, if used, must run entirely client-side against static assets, so the site still deploys as-is to GitHub Pages.
- No CMS, backend, or database — all content is hand-authored in HTML or static files.
- No blog.
- No client-side or server-side contact form — contact is via a `mailto:` link only.
- No separate "About" page. Bio/introduction content lives on the Home/Landing page instead of a standalone page — see Section 5.
- No e-commerce, client login, or password-protected areas.

## 4. Target Audience

- Prospective clients evaluating her for freelance/contract design work.
- Recruiters or hiring managers reviewing her portfolio for full-time roles.
- Peers/collaborators in the design community.

All of these visitors are primarily scanning for: who she is, what her work looks like, and how to contact her — so the site should get out of the way and let the work speak for itself.

## 5. Site Structure / Pages

Based on the selected scope, the initial site includes:

1. **Home / Landing** (also serves as the "About" content — there is no separate About page)
   - Introduces her (name, title/tagline, brief positioning statement, bio).
   - This page absorbs what would otherwise be a standalone "About" page: background, skills, process, or personal statement, as reflected in the provided design.
   - Surfaces or links directly into the work.
   - Should visually match the provided landing page design.

2. **Portfolio / Work Gallery**
   - Displays her design projects (images/assets to be added to the repository).
   - Layout (grid, list, single scrolling page, or individual project detail pages) follows the provided designs — see Open Questions for what's still undecided about structure.

3. **Contact**
   - A `mailto:` link (e.g., `<a href="mailto:her@email.com">`) as the primary call to action.
   - May also include links to relevant social/professional profiles (Instagram, LinkedIn, Behance, Dribbble, etc.) if reflected in the designs.

Primary navigation between pages should use standard HTML links (`<a>` tags) so the site works with links alone. JavaScript may be layered on for supporting UI behavior (e.g., toggling a mobile nav menu) as long as the underlying navigation still works as plain anchors.

## 6. Design Fidelity Requirements

- The designer has produced a set of visual designs and asset files that will be added directly to the GitHub repository (e.g., under an `assets/` or `design/` folder).
- Implementation should adhere closely to these designs: layout, spacing, color palette, typography, and imagery choices should match what's provided, not be reinterpreted.
- Any place where the HTML/CSS implementation must deviate from the source designs (due to web constraints — e.g., font licensing, responsive behavior not specified in a static mockup) should be flagged and resolved with the designer (my wife) before finalizing, rather than assumed.
- Simple interactivity implied by the designs (hover states, focus states) should be implemented with CSS where possible (`:hover`, `:focus`, `:active` pseudo-classes). Where a design implies behavior CSS can't reasonably provide (e.g., a mobile nav toggle, an image lightbox, filtering the portfolio grid), JavaScript may be used — provided it stays client-side only and doesn't introduce animated/motion transitions. If the designs assume animated transitions, those should be simplified to instant state changes.

## 7. Technical Requirements

| Requirement | Detail |
|---|---|
| Languages | HTML5, CSS3, and JavaScript where genuinely needed. JS should be added only for functionality CSS can't reasonably provide (e.g., a mobile nav toggle, image lightbox, portfolio filtering) — not for animation/motion. |
| Site type | Fully static — every page is a hand-authored (or templated) `.html` file with linked `.css` and, if needed, `.js`. No server-side code, backend, or database. |
| Hosting | GitHub Pages, served from the repository (branch/folder to be decided — e.g., `main` branch `/root` or `/docs`, or a `gh-pages` branch). |
| Build step | None strictly required. Since GitHub Pages can serve raw HTML/CSS/JS directly, a compiler/bundler isn't needed unless it meaningfully helps (e.g., a lightweight templating approach to avoid duplicating shared markup like nav/footer). Whatever approach is used, the final output committed to (or generated at deploy time into) the published branch/folder must be plain static files GitHub Pages can serve as-is. |
| Responsiveness | Site should be usable on both desktop and mobile viewports, primarily via CSS (media queries / flexible layouts); JS may assist (e.g., a mobile menu toggle). |
| Browser support | Modern evergreen browsers (Chrome, Firefox, Safari, Edge) — no legacy IE support needed. |
| Performance | Images should be reasonably optimized/sized for web to keep page load fast. JavaScript may be used for progressive enhancements like lazy-loading if it helps. |
| Accessibility | Semantic HTML, meaningful `alt` text on all images, sufficient color contrast per the design palette, logical heading structure. |
| Assets | Images/fonts/other design assets live in the repository (added directly by the designer) and are referenced with relative paths. |

## 8. Content Requirements

- Project images and any supporting copy (project titles, descriptions, categories/tags) will be supplied by the designer and added to the repository.
- Home page copy: name, title/role, short intro/tagline.
- Contact email address to use for the `mailto:` link, plus any social links to include.

## 9. Success Criteria

- Site renders correctly and matches the source designs on both desktop and mobile.
- All pages are reachable via plain HTML navigation with no broken links.
- Site builds/deploys successfully on GitHub Pages with zero build errors.
- Contact link opens the visitor's email client pre-addressed correctly.
- No console errors in the browser dev tools, no layout breakage at common breakpoints.
- Page weight and load time are reasonable (no unnecessarily large unoptimized images).

## 10. Open Questions

- **Portfolio structure:** Should each project have its own detail page, or is the gallery a single scrolling page of images (per the design)? This affects the file structure (one `work.html` vs. `work/project-1.html`, `work/project-2.html`, etc.).
- **Custom domain:** Will the site use the default `github.io` URL, or a custom domain (which would need DNS + a `CNAME` file)?
- **GitHub Pages source:** Which branch/folder will be configured as the Pages source (`main` root, `/docs`, or `gh-pages`)?
- **Favicon / meta tags / social preview (Open Graph) images:** Not yet specified — should be confirmed once designs are reviewed.
- **Repository name/URL:** Needed to finalize the GitHub Pages URL structure.

## 11. Out of Scope / Explicitly Not Building

- Animations or motion-based transitions, whether implemented in CSS or JavaScript.
- Any backend, server, or database — JavaScript, where used, is client-side only against static assets.
- Contact forms with server-side processing (contact remains a `mailto:` link).
- CMS or admin interface for updating content.
- Analytics/tracking (unless later requested — if added, should be a lightweight, static-compatible option that doesn't require a backend).