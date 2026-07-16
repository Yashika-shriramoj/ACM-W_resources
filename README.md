# ACM-W BPHC — Domain Pages

Subject-domain pages for the ACM-W BITS Pilani Hyderabad Campus chapter website. Each page covers one learning track (e.g. **Machine Learning & AI**) with study resources, domain projects, and mentor info — matching the theme of the chapter's main site (`index.html`).

## What's in here

| File | Purpose |
|---|---|
| `ml-ai.html` | Domain page for Machine Learning & AI — name, blurb, resources, projects, mentors |
| `study.html` | Reusable template that renders study material for **any** topic, based on a URL parameter |
| `domain-page.css` | Styles for resource cards, project flip cards, and mentor cards — built on the color/font variables already defined in `style.css` |
| `domain-page.js` | Header behavior for these standalone pages (theme toggle, mobile nav, domains dropdown) plus flip-card click/tap handling |
| `study.js` | Topic → content lookup used by `study.html` |

These pages depend on the main site's `style.css` (for design tokens like `--ink`, `--magenta`, fonts, etc.) — they don't duplicate it.

## Setup

1. Copy all five files into the same folder as the main site's `index.html`, `style.css`, and `script.js`.
2. Open `ml-ai.html` in a browser to check it — no build step needed, everything is static HTML/CSS/JS.
3. Note: `script.js` from the homepage is **not** loaded on these pages. It's built around `index.html`'s single-page tab system and calendar, and isn't needed here. `domain-page.js` covers what these pages actually use (theme toggle, nav, dropdown, flip cards).

## How the study material template works

Resource cards link to `study.html?topic=<slug>`, e.g.:

```html
<a class="resource-card" href="study.html?topic=neural-networks">...</a>
```

`study.js` reads that slug from the URL and looks it up in the `TOPICS` object to populate the title, intro, and (currently lorem ipsum) body content.

### Adding a new topic to an existing domain

1. Add a new `.resource-card` link in the domain's HTML file pointing to `study.html?topic=your-slug`.
2. Add a matching entry to the `TOPICS` object in `study.js`:

```js
"your-slug": {
  domainLabel: "Machine Learning & AI",
  domainHref: "ml-ai.html",
  title: "Your Topic Title",
  intro: "One-line description of the topic.",
},
```

3. Replace the lorem ipsum in `LOREM_SECTIONS` (or swap in per-topic content) once real material is ready.

## Adding a new domain page (e.g. Web Development, Cybersecurity)

1. Duplicate `ml-ai.html` and rename it (e.g. `web-dev.html`).
2. Update:
   - Page `<title>` and meta description
   - The domain name (`<h1 class="page-hero-title">`) and intro blurb
   - The 4–5 resource cards (topic names + `study.html?topic=` links)
   - The 2–3 project flip cards (image, name, description)
   - The mentors list
3. Add the new topics to `TOPICS` in `study.js`, pointing `domainHref` at the new file.
4. Link the new domain page from wherever your site's navigation lists domains.

## Design notes

- Colors, fonts, and spacing all come from the CSS variables defined in the homepage's `style.css` (`--ink`, `--magenta`, `--violet`, `--font-display`, `--font-body`, etc.), so these pages automatically match the current theme and support the same light/dark mode toggle.
- Placeholder project images use [placehold.co](https://placehold.co) — swap in real project screenshots when available.
- Flip cards work on click/tap and keyboard (Enter/Space), not just hover, so they behave the same on mobile and desktop.

## Known follow-ups

- Nav links point to `index.html#about`, `index.html#events`, etc. — confirm this matches the actual filename of the homepage in the deployed repo.
- `domainHref` values in `study.js` currently only point to `ml-ai.html`. Update them as new domain pages are added.
- Replace lorem ipsum in `study.js` with real study content per topic.
