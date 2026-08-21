# Page Contract: Work Gallery & Project Detail Pages

This static site has no API; the "contract" here is the fixed HTML
structure and linking convention that `work.html` and every `work/*.html`
detail page must follow, so navigation stays consistent (spec FR-001,
FR-004, FR-006) and future projects can be added without touching layout
(constitution Principle V).

## `work.html` (Work Grid)

**Required structure**:

```html
<header class="site-header">...</header>          <!-- identical to index.html's header -->
<div class="wave-divider" aria-hidden="true"></div> <!-- identical to index.html -->

<main class="work-main">
  <ul class="work-grid">
    <li class="work-tile">
      <a href="work/<slug>.html">
        <img src="assets/images/<assetFolder>/<thumbnail>" alt="<title> project thumbnail" />
        <span class="work-tile-title"><title></span>
      </a>
    </li>
    <!-- one <li> per Project, in Project Catalog order (data-model.md) -->
  </ul>
</main>

<footer class="site-footer">...</footer>          <!-- identical to index.html's footer -->
```

**Contract guarantees**:
- Exactly 10 `<li class="work-tile">` entries, in Project Catalog order.
- Every tile's `<a href>` points to `work/<slug>.html` for that project.
- Every tile's `<img src>` points to that project's `thumbnail` path from
  `data-model.md`.
- Header/footer markup is byte-for-byte reused from `index.html` (same
  nav links, same logo, same footer text) so site chrome is consistent.

## `work/<slug>.html` (Project Detail Page)

**Required structure**:

```html
<header class="site-header">...</header>          <!-- identical to index.html's header -->
<div class="wave-divider" aria-hidden="true"></div>

<main class="project-detail">
  <a class="back-to-work" href="../work.html">&larr; Back to Work</a>
  <h1><title></h1>
  <div class="project-detail-images">
    <img src="../assets/images/<assetFolder>/<image>" alt="<title> - <descriptive detail>" />
    <!-- one <img> per entry in that Project's detailImages list -->
  </div>
</main>

<footer class="site-footer">...</footer>
```

**Contract guarantees**:
- Filename is exactly `work/<slug>.html` where `<slug>` matches the
  Project Catalog entry in `data-model.md`.
- Contains a back-link to `work.html` (FR-006), reachable and focusable via
  keyboard.
- Renders every image in that Project's `detailImages` list and no images
  from any other project (spec SC-003).
- `<h1>` text equals the Project's `title`.
- Reuses the same header/footer markup as `work.html` and `index.html`.

## Linking convention

- Grid → detail: relative path `work/<slug>.html` (from repo root, where
  `work.html` lives).
- Detail → grid: relative path `../work.html` (from inside `work/`).
- Detail → images: relative path `../assets/images/<assetFolder>/<file>`
  (from inside `work/`).
- Header nav's existing "Work" link (`work.html` in `index.html`, and the
  equivalent on every detail page) is the only entry point from outside
  this feature; no other page links directly into `work/*.html`.
