# Alejandro Rodriguez — Portfolio

Personal portfolio site for Alejandro Rodriguez Orama (Data Analyst / Data Scientist, Windsor, Ontario).
Live at **https://arol9204.github.io/**.

## Stack

Static HTML, one hand-written stylesheet, ~80 lines of vanilla JS. No frameworks, no build step, no jQuery.
GitHub Pages serves the repository root as-is.

| Path | What it is |
| --- | --- |
| `index.html` | Single-page portfolio: hero, work, skills, experience, background, contact |
| `project_details_*.html` | Case-study pages, one per project |
| `Project1.html` | Self-contained R Markdown report (Fuel Consumption EDA) |
| `assets/css/site.css` | The design system — tokens, layout, components |
| `assets/js/site.js` | Theme toggle, sticky nav, scroll-spy, reveal-on-scroll |
| `images/` | Project screenshots, portrait, résumé PDF |

## Design system

Everything is driven by CSS custom properties defined at the top of `assets/css/site.css`:

- **Colour** — `--bg`, `--bg-elev`, `--ink`, `--line`, `--accent`. Light values live on bare `:root`;
  dark values are redefined twice, once under `prefers-color-scheme: dark` and once under
  `:root[data-theme="dark"]`, so the manual toggle wins in both directions.
- **Type** — Inter for text, JetBrains Mono for labels and figures, both from Google Fonts with
  system-font fallbacks.
- **Shape** — `--radius`, `--radius-sm`, `--radius-lg` and three shadow steps.

Changing the accent colour across the whole site is a two-line edit (`--accent` in `:root` and in the
dark blocks).

## Editing

**Add a project** — copy an `<article class="card reveal">` block in `index.html` under `#work`, then copy
one of the `project_details_*.html` files as the case-study page. Case studies use `.prose` for body copy,
`.figure` for screenshots, `ol.steps` for numbered walkthroughs and `ul.bullets` for takeaways.

`#work` has two tiers. The top grid holds public projects: image, badge, chips and links out to a case
study. Below the "Shipped in production" subheading is a second grid of `.card.card-compact` blocks — the
same card with no `.card-media` and no detail page, for internal work that has no shareable screenshot.
A compact card uses `.card-tag` for its category line and `.card-note` for the status line in the footer.
Give one a case-study page and it graduates to the top grid.

**Skills** are grouped by category, one `.skill-card` per group, each holding `.chip` tokens. Marking the
two or three leading tools in a group with `chip-accent` is what keeps a long list scannable.

**Update the résumé** — replace the PDF in `images/` keeping the same filename, or update the two links in
`index.html` (nav and contact section).

**Theme** — the user's choice is stored in `localStorage` under `theme`; an inline script in each `<head>`
applies it before first paint so there is no flash.

## Local preview

No server needed — open `index.html` in a browser. To serve it over HTTP instead, any static server works
(e.g. `npx serve .`).

## Notes

- `others designs/` holds the original HTML5 UP templates the previous version of this site was built on.
  Nothing in the live site references them any more.
- Screenshots in `images/` are full-resolution PNGs; all of them are lazy-loaded, but compressing the
  largest ones would make the case-study pages noticeably faster.
