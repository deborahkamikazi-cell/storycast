# StoryCast

## 1. Project overview

StoryCast is a university assignment: a three-page educational microsite
dedicated to historical remembrance and education about **the 1994 Genocide
against the Tutsi in Rwanda**. This build implements the three Figma
screenshots (Home, Story Detail, About & Accessibility) provided for the
project as closely as possible, using only **HTML5, Sass/SCSS, and compiled
CSS — no JavaScript, no Node.js runtime dependency, and no frontend
framework.**

Read this together with
["Known limitations & deviations from the Figma screenshots"](#14-known-limitations--deviations-from-the-figma-screenshots)
below before assuming any piece of content is final — several specific
details from the screenshots were intentionally replaced with honest
placeholders; see that section for the full list and reasoning.

## 2. Technologies used

- HTML5 (semantic markup)
- Sass/SCSS — modern `@use` module system, CSS cascade layers
- CSS3 — Grid, Flexbox, Container Queries, and the `:has()` relational
  pseudo-class (used for real, JavaScript-free accessibility toggles)
- **No JavaScript** anywhere on the site, and no Node.js/npm artifacts are
  part of the project (no `package.json`, no `node_modules/`). Sass is
  compiled with a standalone/ephemeral Sass tool — see
  [§9](#9-how-to-compile-sass-without-a-project-level-nodenpm-dependency).

**No frontend framework is used** (no React, Vue, Angular, Bootstrap, or
Tailwind).

## 3. Folder structure

```
storycast/
├── index.html
├── about.html
├── story/
│   └── remembering-1994.html
├── sass/
│   ├── main.scss
│   ├── _colors.scss
│   ├── _typography.scss
│   ├── _spacing.scss
│   ├── _reset.scss
│   ├── _layout.scss
│   ├── _components.scss
│   └── _accessibility.scss
├── css/
│   └── main.css           (compiled — do not edit directly)
├── assets/
│   ├── images/ audio/ video/ captions/ transcripts/   (all currently empty)
├── docs/
│   ├── sitemap.md
│   ├── research-notes.md
│   ├── design-links.md
│   └── accessibility-checklist.md
└── .gitignore
```

## 4. The three pages

1. **Home — `index.html`** — utility ribbon, header with "Audio Guide" and
   a working CSS-only "Accessibility Mode" toggle, hero, a disabled
   search/filter preview (clearly labeled as non-functional), the
   "Voices of Survival" featured-media card, three educational feature
   cards, a pull-quote banner, and a commemoration banner.
2. **Story Detail — `story/remembering-1994.html`** — story meta, working
   CSS-only Text Scale and Readability Font Mode controls, a media player
   prepared for native `<video>`/`<audio>` + `<track>` (commented until
   real files exist), a transcript with sidebar (archival log, speaker
   profile, linguistic note), historical context, a location/provenance
   verification section, reserved related-content slots, references, and a
   citation block.
3. **About & Accessibility — `about.html`** — mission statement, three
   ethical "pillars," three education-audience cards, four WCAG feature
   cards (honestly marked Planned/Implemented), a real working `mailto:`
   feedback form, and an advisory council section with four **unfilled**
   seats.

Full information architecture: [`docs/sitemap.md`](docs/sitemap.md).

## 5. Setup & running locally

No install step is required to view the site — it is static HTML/CSS. Serve
the folder with any static file server, or open the files directly in a
browser:

```bash
python3 -m http.server 8000
# or
npx --yes serve .
```

Then visit `http://localhost:8000/index.html`.

## 6. How Sass is organized

Modern `@use` (no deprecated `@import`), 8 partials, 5 CSS cascade layers
(`reset < base < layout < components < utilities`), BEM naming throughout.
Tokens (`_colors.scss`, `_typography.scss`, `_spacing.scss`) were set to
match the Figma screenshots: a warm cream "archival paper" background,
near-black ink text, a muted olive-green accent for "verified/synced"
states, a serif heading face paired with a sans body face (system font
stacks — see [§14](#14-known-limitations--deviations-from-the-figma-screenshots)),
and a spacing scale matching the screenshots' rhythm.

## 7. Where CSS Grid and Flexbox are used

- **Flexbox**: header/nav bar, footer columns' internal content, card
  internals, the accessibility-controls row, the search/filter bar.
- **CSS Grid**: `.card-grid` (story/feature/related cards, 1→2→3 columns
  responsively), the footer's 4-column layout, the two-column
  transcript/verification layouts on wide screens, the mission-split and
  advisory-council grids.

## 8. The CSS Container Query

`.card-grid` (used for the featured story card, the three educational
cards, the WCAG feature cards, and the "Voices from the Western Province"
related cards) is declared as an inline-size containment context in
`sass/_layout.scss`:

```scss
.card-grid {
  container-type: inline-size;
  container-name: card-grid;
}
```

`sass/_components.scss` then queries that container, not the viewport:

```scss
@container card-grid (max-width: 26rem) {
  .story-card {
    flex-direction: column;
  }
}
```

**Why:** `.story-card` (the homepage's featured-story layout) defaults to a
horizontal layout. When the card's own available width drops below
`26rem` — on a narrow phone, or even on a wide desktop once the grid places
two or three cards per row — it switches to a vertical, stacked layout. A
plain viewport media query cannot do this, because it only knows the full
browser width, not the width actually available to this one component.
Verified in-browser with Playwright: the card renders in column layout at a
390px viewport and row layout at 768px/1440px.

## 9. How to compile Sass without a project-level Node/npm dependency

This project does not ship a `package.json`, `package-lock.json`, or
`node_modules/` — none of those files exist in the repository, by design.
To compile `sass/main.scss` → `css/main.css`, use **one** of:

**Option A — Dart Sass standalone executable (recommended, no Node.js at
all).** Download the standalone build for your OS from the
[Dart Sass releases page](https://github.com/sass/dart-sass/releases) (it
ships as a single self-contained binary, not an npm package), then run:

```bash
/path/to/dart-sass sass/main.scss css/main.css --no-source-map --style=expanded
```

**Option B — VS Code "Live Sass Compiler" extension.** Install the
extension, open `sass/main.scss`, and click "Watch Sass" in the status bar.
Configure its output path to `css/main.css` if prompted.

**Option C — `npx` (if Node.js happens to be installed on your machine).**
`npx` downloads and runs the Sass CLI from its own cache without adding any
file to this project:

```bash
npx --yes sass sass/main.scss css/main.css --no-source-map --style=expanded
```

This is how `css/main.css` was generated and validated during development
of this project — it leaves no `package.json`/`node_modules` behind.

## 10. Accessibility — what's real vs. planned

See [`docs/accessibility-checklist.md`](docs/accessibility-checklist.md) for
the complete, honestly-labeled list. Headline items:

- **Implemented and verified:** semantic landmarks, one `<h1>`/`<main>` per
  page, logical heading order, a working skip link, visible focus states,
  reduced motion support, no horizontal overflow at 390/768/1440px, and —
  notably — **three fully-functional, JavaScript-free accessibility
  controls** (Text Scale, Readability Font Mode, sitewide Accessibility
  Mode) built with native `<input>` elements and the CSS `:has()`
  relational pseudo-class. These were tested in-browser by reading computed
  styles before/after toggling, not just visually.
- **Not yet done:** a formal WCAG 2.1 AA test/audit, real captions/
  transcripts, real alt text (no real images exist yet), and a verified
  contrast audit. Every badge on the site says "Targeting WCAG 2.1 AA," not
  "Verified" or "Compliant."

## 11. Media & transcript status

Two real testimony videos are now embedded, via the standard YouTube
`iframe` embed (not downloaded or re-hosted):

- **Home page** — "Testimony of a Genocide Survivor from Rwanda," published
  by the United Nations.
- **Story Detail page** — the testimony of Béatha Mukarubuga ("Maman
  Lambert"), published by Aegis Trust (which manages the Kigali Genocide
  Memorial).

Both were confirmed via YouTube's public oEmbed metadata before use. No
file has been copied into this repository — `assets/video/`, `assets/audio/`,
`assets/captions/`, and `assets/transcripts/` remain empty, and the
`<video>`/`<audio>`/`<track>` markup prepared for a *future self-hosted*
recording is still present as commented-out example code. StoryCast has
**not** produced its own transcript for either embedded video — captions
depend entirely on what the publisher has uploaded to YouTube, accessible
via the player's own CC button. See
[`docs/research-notes.md`](docs/research-notes.md) for the full source log.

## 12. Validation performed this session

- `npx html-validate` on all three pages: **0 errors.**
- Sass compiled cleanly with no errors or warnings.
- Playwright-driven checks: no horizontal overflow at 390px/768px/1440px on
  any page; container query confirmed functional; skip link confirmed
  functional (off-screen until focused); all three CSS-only accessibility
  toggles confirmed functional via `getComputedStyle` before/after
  toggling; heading hierarchy and landmark structure inspected via the
  accessibility tree on all three pages.
- Manual review confirmed no `package.json`/`node_modules`/JavaScript files
  exist anywhere in the project.
- **Not performed:** a real screen-reader pass, a formal contrast audit, and
  cross-browser testing of the `:has()`-based controls beyond a
  Chromium-based browser.

## 13. Remaining tasks before submission

- [ ] Replace all placeholder media/images once real, rights-cleared assets
      exist.
- [ ] Complete verified historical research and citations
      ([`docs/research-notes.md`](docs/research-notes.md)).
- [ ] Fill the advisory council seats only with people who have actually
      agreed to the role, or remove the section.
- [ ] Run a real accessibility audit (axe/Lighthouse + manual screen reader
      + keyboard pass) and update the checklist.
- [ ] If a live Figma link becomes available, reconcile it against
      [`docs/design-links.md`](docs/design-links.md).

## 14. Known limitations & deviations from the Figma screenshots

The Figma screenshots were followed closely for **layout, color, typography,
spacing, component structure, and section order**. A specific, limited set
of **content details** were intentionally changed, because reproducing them
literally would have meant publishing misinformation:

| Figma showed | This build uses instead | Why |
|---|---|---|
| A named survivor ("Claudine Mukamana") with a specific quoted testimony and biography | Generic placeholders ("Narrator — name pending verified consent") with the same layout | No real survivor or testimony was provided; inventing one would be fabricated testimony about a real genocide. |
| A "WCAG 2.1 AA VERIFIED" badge | "Targeting WCAG 2.1 AA" | No formal accessibility audit has been performed yet. |
| Specific GPS coordinates, SHA-256 hash fragments, checksum dates, and accession numbers presented as verified archival data | "Not yet assigned" / "Map to be added" / general region names only | These implied a level of verification and audit that has not happened. |
| An "Advisory Council" naming real, identifiable historians (e.g. a named genocide historian and a named academic) as endorsers | Role titles only, each marked "Seat unfilled — pending appointment" | Naming real people as advisors/endorsers without their knowledge or consent would misattribute a real person's name to a fictional project. |
| A custom-styled media player UI (scrubber, caption toggle, speed control) | For the two real testimonies: the standard YouTube `iframe` embed, which gives a real, working, keyboard-accessible native player for free. For any *future self-hosted* clip: `<video controls>` / `<audio controls>` (prepared, commented until a file exists). | This project uses no JavaScript, and a custom player UI that doesn't actually play/scrub anything would be a non-functional, misleading control. |
| A functional-looking search/filter bar returning "1,249 documented testimonies" | The same layout, with all controls `disabled` and an honest note that search isn't implemented | The site contains exactly one placeholder story; claiming a large searchable corpus would be misleading. |
| "Copy Citation"/clipboard-copy buttons | Selectable text with a "select to copy" note | Clipboard copy requires JavaScript, which this project does not use. |
| Exact Figma font files | System serif/sans stacks (Georgia-based heading stack, system-ui body stack) | No font files or Google Fonts link were supplied, and adding a web-font dependency wasn't part of the brief. |

Everything else — the ribbon/header pattern, hero layout, card grids, pillar
list, feedback form, footer structure, and overall tone — follows the
screenshots directly.
