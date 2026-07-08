# How to Update Your Portfolio

A step-by-step guide for adding projects, swapping images, and editing your About page — no coding required.

---

## What you need (one-time setup)

1. **GitHub Desktop** — download at [desktop.github.com](https://desktop.github.com)
2. **A text editor** — TextEdit (Mac) works fine, but [Visual Studio Code](https://code.visualstudio.com) is easier because it colour-codes the file
3. **The repo cloned to your Mac** — Rick can do this for you. It will create a folder called `project-portfolio` somewhere on your computer
4. **Task** (optional, but makes things easier) — Rick can install this for you with one command: `brew install go-task`

---

## Shortcuts (once Task is installed)

Open Terminal, navigate to the `project-portfolio` folder, and use these two commands:

| Command | What it does |
|---|---|
| `task run` | Opens a live preview of the site in your browser. Press Ctrl+C to stop. |
| `task copy NAME=my-project-name` | Creates a new project folder from the template and opens it in Finder. |

**Example:**
```
task copy NAME=coastal-hotel-rebrand
```
This creates `content/work/coastal-hotel-rebrand/`, pre-filled with the template, and pops the folder open in Finder ready for you to drop images in.

> **Tip:** Replace spaces with hyphens in the name, and use lowercase only.
> `coastal-hotel-rebrand` ✅ — `Coastal Hotel Rebrand` ❌

---

## The golden rule

**Always sync before you start, and push when you're done.**

In GitHub Desktop:
- Click **Fetch origin** (top bar) before starting any work
- Click **Push origin** when you're done

If you forget to fetch first and someone else made a change, GitHub Desktop will warn you and walk you through it.

---

## Adding a new project

### 1. Create the project folder

**With Task (fast):** In Terminal, run:
```
task copy NAME=my-project-name
```
This creates the folder with the template already inside and opens it in Finder. Skip to step 2.

**Without Task (manual):** Open Finder, go to `content → work`, and create a new folder by hand. Use lowercase letters and hyphens only — no spaces, no capital letters.
✅ `coastal-hotel-rebrand` — ❌ `Coastal Hotel Rebrand`

Then copy the file `archetypes/work/index.md` into your new folder.

### 2. Prepare your images

Before copying anything in, rename your images like this:

| File | What it's for |
|---|---|
| `cover.jpg` | The image shown on the Work grid |
| `gallery-1.jpg` | First gallery image on the project page |
| `gallery-2.jpg` | Second gallery image |
| `gallery-3.jpg` | Third gallery image (add as many as you need) |

**Image tips:**
- Export as **JPG** at full resolution — the site automatically creates smaller sizes for fast loading
- The cover image works best in landscape orientation (wider than tall)
- Gallery images can be any orientation
- File size doesn't matter much — bigger is fine, the site handles it

Copy all your renamed images into your new project folder.

### 3. Fill in the project info file

Open `index.md` (already in your project folder) in your text editor. It will look like this:

```
+++
title    = "Brand Identity"
date     = 2024-03-15T00:00:00Z
draft    = false

year     = 2024
client   = "Studio Maison"
role     = "Art Direction, Brand Identity"
summary  = "A complete visual identity system..."

flagship = true

challenge = "..."
solution  = "..."
+++
```

Edit each field:

| Field | What to put |
|---|---|
| `title` | The project name as you want it displayed |
| `date` | The date the project was completed — format: `2024-06-01T00:00:00Z` |
| `draft` | Keep as `false` so it shows on the site |
| `year` | Just the year number, no quotes: `2024` |
| `client` | Client name in quotes: `"Maison Hotel"` |
| `role` | Your role in quotes: `"Art Direction, Print Design"` |
| `summary` | One sentence about the project, in quotes |
| `tags` | Labels in square brackets: `["Branding", "Print"]` |
| `flagship` | `true` for a full case study, `false` for image-only |
| `challenge` | (Flagship only) The problem you were solving |
| `solution` | (Flagship only) How you solved it |

> **Important:** Keep all the `+++` lines exactly as they are — at the very top and after the last field. Don't delete them.

#### Flagship vs regular

- **`flagship = false`** — shows a hero image and gallery. Best for most projects.
- **`flagship = true`** — adds "The Challenge" and "The Solution" sections above the gallery. Use for your most in-depth case studies. Requires the `challenge` and `solution` fields.

If a project is not flagship, you can delete the `challenge` and `solution` lines entirely.

### 4. Your folder should look like this

```
content/work/coastal-hotel-rebrand/
  index.md
  cover.jpg
  gallery-1.jpg
  gallery-2.jpg
  gallery-3.jpg
```

### 5. Publish it

Open GitHub Desktop. You'll see your new files listed on the left.

1. At the bottom left, type a short description in the **Summary** box — e.g. `Add coastal hotel project`
2. Click **Commit to main**
3. Click **Push origin** (top bar)

The site rebuilds automatically and will be live within a minute or two.

---

## Updating the About page

Open the file:

```
content → about.md
```

The top section (between the `+++` marks) controls the skills lists. Edit the items inside the square brackets.

The text below the second `+++` is your bio. Edit it like a normal document — line breaks become paragraphs.

To add a **portrait photo**: name your photo `portrait.jpg` (or any image format) and set the `portrait` field to its filename. Place the photo in the `content/` folder alongside `about.md`.

To add a **downloadable CV**: put a PDF file in the `static/files/` folder and set `resumeURL = "/files/your-filename.pdf"`.

Save the file, then commit and push in GitHub Desktop (same as step 6 above).

---

## Updating social links or email

Open the file `hugo.toml` (it's in the main `project-portfolio` folder, not inside `content`).

Find this section:

```toml
[params]
  email = "shelley.cerny@gmail.com"

  [params.social]
    instagram = ""
    behance   = ""
    linkedin  = ""
```

Paste your profile URLs between the quotes. Leave a field as `""` (empty) if you don't use that platform — it won't show up on the site.

---

## Changing the order projects appear

Projects are sorted by `date` — newest first. To move a project up or down on the grid, change its `date` in the `index.md` file.

---

## Preview before publishing

Run `task run` in Terminal. A browser window will open showing the site exactly as it will look when live, including any unpublished drafts. Press Ctrl+C when you're done.

---

## Something looks wrong?

- **Project not showing:** Make sure `draft = false` in the `index.md`
- **Images not showing:** Double-check the filenames — `cover.jpg` and `gallery-1.jpg` must be spelled exactly right, all lowercase
- **Page looks broken:** You may have accidentally deleted a `+++` line or a quote mark. Compare your file to a working project's `index.md`

If something's really stuck, message Rick — he can look at the file and spot the issue in seconds.
