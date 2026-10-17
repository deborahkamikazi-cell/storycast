# StoryCast — Accessibility Checklist (WCAG 2.1 AA)

This checklist tracks accessibility work for StoryCast. **This site has not
undergone formal WCAG 2.1 AA testing or certification.** The ribbon/footer
badges on every page intentionally say "Targeting WCAG 2.1 AA," not
"Verified" or "Compliant" — the Figma screenshots showed a "WCAG 2.1 AA
VERIFIED" badge, which this project does not use because that claim has not
been earned yet.

## Implemented and verified in this session

- [x] Semantic landmarks (`header`, `nav`, `main`, `section`, `article`,
      `aside`, `footer`) on all three pages, each `aside` given a unique
      accessible name (`html-validate` confirms no duplicate-landmark
      errors).
- [x] One `<main>` landmark and one `<h1>` per page; logical heading order
      (h1 → h2 → h3 → h4) with no skipped levels — spot-checked via the
      browser accessibility tree on all three pages.
- [x] Skip-to-main-content link on every page, confirmed via automated
      check: hidden at `top: -48px` until focused, then `top: 0`.
- [x] Keyboard-accessible navigation using native links only — no custom
      widgets, no keyboard traps.
- [x] Visible `:focus-visible` outline on interactive elements.
- [x] Descriptive link text (e.g. "Open Full Story & Transcript" rather than
      "click here").
- [x] `lang="en"` set on every page; UTF-8 charset and responsive viewport
      meta tags present on every page.
- [x] Unique, descriptive `<title>` and `<meta name="description">` per
      page.
- [x] Reduced-motion support via `prefers-reduced-motion`.
- [x] Responsive, fluid text sizing and layout at mobile/tablet/desktop
      widths — confirmed with Playwright: no horizontal overflow at 390px,
      768px, or 1440px on any of the three pages.
- [x] **CSS-only, fully functional accessibility controls (no JavaScript):**
      a Text Scale radio group (A− / A / A+) and a Readability Font Mode
      toggle on the Story Detail page, and a sitewide Accessibility Mode
      toggle in the header — all built with native `<input type="radio">` /
      `<input type="checkbox">` plus the `:has()` relational pseudo-class.
      Verified in-browser: toggling each control measurably changes
      `--user-font-scale`, `font-family`, and `line-height` via
      `getComputedStyle`. In browsers without `:has()` support, the controls
      remain visible, labeled, and focusable — they simply have no visual
      effect yet (graceful degradation, never a broken/fake control).
- [x] Two testimony videos are embedded via the standard YouTube `iframe`
      embed method (`index.html` and the Story Detail page) rather than
      downloaded/re-hosted files — this is the publisher-sanctioned sharing
      method, and it gives visitors YouTube's own native player: a working
      CC/captions button (when the publisher has captions), keyboard
      operability, fullscreen, and playback-speed controls, all for free and
      without any JavaScript written by this project. StoryCast has not
      independently verified caption presence or accuracy for either video —
      see `research-notes.md`.
- [x] The feedback form on `about.html` is a real, working HTML form
      (`action="mailto:..." enctype="text/plain"`) — submitting it opens the
      visitor's email client with the report pre-filled. No fake/inert
      submit button.
- [x] Disabled form controls (the homepage search/filter bar) use the native
      `disabled` attribute, which both visually indicates and
      programmatically announces (to assistive tech) that the control is
      inactive, rather than silently pretending to work.
- [x] Temporary neutral color tokens chosen for AA-oriented contrast (see
      `sass/_colors.scss`) pending a confirmed formal contrast audit.
- [x] No ARIA roles added to native elements that already expose the correct
      semantics (e.g. no `role="navigation"` on `<nav>`).

## Pending — requires real content/media or formal testing

- [ ] Produce and attach real WebVTT caption files for any future
      self-hosted video (the two videos currently on the site are embedded
      externally from YouTube and use that platform's own caption system).
- [ ] Produce and attach real, verified transcripts for the two embedded
      testimonies, with the original publishers' involvement.
- [x] The home-page hero now has a real `<img>` with descriptive `alt` text
      (see `docs/research-notes.md` for its unresolved rights status —
      **do not treat this as "done" for submission purposes** until that is
      resolved).
- [ ] Formal automated accessibility scan (axe, Lighthouse) against the
      final content and design.
- [ ] Manual screen reader testing (VoiceOver, NVDA) across all three pages.
- [ ] Manual keyboard-only navigation walkthrough of the final site.
- [ ] Formal color-contrast audit (a tool-based contrast check has not been
      run in this session; the palette was chosen for likely AA contrast
      but this is not the same as a verified audit).
- [ ] Re-test `:has()`-dependent controls in a wider spread of real browsers
      and screen readers (tested in this session with a Chromium-based
      browser only).

**Do not mark this project as WCAG 2.1 AA compliant until every item above
has been completed and verified.**

## A note on the advisory council and testimony content

The Figma screenshots shown to build this site included a specific named
survivor with an invented quotation, specific "verified" archival metadata
(hashes, accession numbers, GPS coordinates), and an advisory board listing
real, identifiable genocide historians as if they had reviewed and endorsed
this project. None of that was real. This build intentionally replaced
those specifics with honest placeholders (e.g. "Seat unfilled — pending
appointment," "Not yet assigned") while keeping the same layout and
component structure, because presenting fabricated testimony or an
unconsented endorsement as real would itself be a serious accessibility and
integrity failure — accessible design that misleads visitors is not
accessible in any meaningful sense. See the README's "Known limitations &
deviations from the Figma screenshots" section for the full list.
