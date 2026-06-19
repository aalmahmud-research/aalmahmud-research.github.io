# Research Portfolio Website

A single-page academic/research portfolio. All visible content lives in **JSON files** —
you almost never need to touch `index.html`. Edit the JSON, drop in your images, done.

## How it works

`index.html` is a template. When the page loads, its JavaScript fetches the JSON files
below and renders each section. Sections: About → News → Research Interests → Education →
Experience → Publications → Projects → Contact.

```
portfolio/
├── index.html              ← the template (rarely edited)
├── config.json             ← layout/sizing knobs + news highlight colors
├── about.json              ← name, bio, photo, skills, social links, CV link
├── news.json               ← timeline of updates
├── research_interest.json  ← research area cards
├── education.json          ← degrees
├── experience.json         ← jobs / positions
├── publications.json       ← papers (with collapsible abstracts)
├── projects.json           ← project cards
└── media/                  ← all images, logos, and your CV PDF
```

## Run it locally

The page loads data with `fetch()`, which **does not work if you double-click the HTML
file** (`file://`). You must serve it over HTTP. From inside the `portfolio/` folder:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Any static server works (`npx serve`, VS Code "Live
Server" extension, etc.).

## Publish free on GitHub Pages

1. Create a repo named `your-username.github.io`.
2. Put all these files at the repo root and push.
3. In the repo: **Settings → Pages → Branch: main → /(root) → Save**.
4. Visit `https://your-username.github.io` (takes a minute the first time).

## What to edit

### about.json
Your name, title, bio, photo path, location, email, CV link, skill chips, and social links.
- **Advisor link (optional):** set `advisor_name` to the exact name as it appears in your
  `bio`, and `advisor_link` to their URL. That name becomes a clickable link automatically.
- **Skill chip colors:** the `colors` field uses Tailwind classes, e.g.
  `"bg-green-100 text-green-800"`. Swap the color word (blue, indigo, purple, red, etc.).

### config.json
- `profilePictureSize` — profile photo size in px.
- `publicationThumbnailWidth` — width of paper thumbnails (e.g. `"20%"`).
- `sectionSpacingY` — vertical padding between sections.
- `aboutBackgroundImage` — `null`, or a path like `"media/banner.jpg"` for a hero banner.
- `newsHighlights` — auto-highlight keywords in news text. Each entry maps a phrase to a
  `color` + `background`, e.g. `"NeurIPS 2025": { "color": "#6d28d9", "background": "#f5f0ff" }`.

### publications.json
Each paper supports: `status` (badge text, leave `""` for none), `status_colors`,
`year`, `title`, `authors`, `conference`, `thumbnail`, `description` (the abstract),
`tags`, and three optional links: `paper_link`, `project_link`, `github_link`.
Set any link to `null` (or omit) to hide that button.

### projects.json
`name`, `image`, `stacks` (tech tag list), `github_link`, `details_page`.
Empty string `""` or omit a link to hide its button.

## Images

Replace the placeholder files in `media/` with your own (keep the same filenames, or
update the paths in the JSON). Recommended:
- Profile photo: square, ~500×500.
- Research images: landscape, ~600×400.
- Paper thumbnails: portrait, ~400×520.
- Logos: square PNG with transparent background.
- Your CV: replace `media/pdf/CV.pdf`.

## Customizing colors / fonts

The accent color is blue/indigo throughout (Tailwind `blue-600`, `indigo-400`, etc.).
To re-theme, find-and-replace those class names in `index.html`, and adjust the gradient
hex values in the `<style>` block at the top (`gradient-heading`, `#scroll-progress`,
`#scroll-to-top`).

## Dependencies

Loaded from CDN in `index.html` (nothing to install):
- Tailwind CSS (Play CDN)
- Lucide icons
- Inter font (Google Fonts)

For a fully offline / production build you can vendor these into local files and swap the
CDN `<script>`/`<link>` tags accordingly.
