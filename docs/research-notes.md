# StoryCast — Research Notes

## Research objective

To responsibly present the history of the 1994 Genocide against the Tutsi in
Rwanda, every factual claim, survivor testimony, media clip, and citation
published on StoryCast must be sourced from verified, reputable material
before it is added to the site. **No historical content in this foundation
phase has been verified yet** — the story page currently contains only
placeholder text pending this research.

## Historical source checklist

Status: ☐ not started · ☑ in progress · ✅ verified

- [ ] Identify reputable primary and secondary historical sources (e.g.
      recognized genocide memorial institutions, academic publications,
      established human-rights organizations).
- [ ] Cross-check factual claims (dates, figures, locations) across at least
      two independent reputable sources.
- [ ] Record the full citation (author/organization, title, publisher, date,
      URL or archive reference) for every source used.
- [ ] Review historical terminology for accuracy and respectfulness.
- [ ] Have content reviewed before publishing to the live story page.

## Media sourcing checklist

- [ ] Confirm the origin and rights status of any video or audio testimony.
- [ ] Obtain explicit permission/license for any survivor testimony used.
- [ ] Verify that media is directly relevant to this project (no unrelated
      stock or sample footage).
- [ ] Produce or source a verified WebVTT caption file for every video.
- [ ] Produce or source a verified transcript for every audio/video item.
- [ ] Store original media files in `assets/video/` or `assets/audio/`,
      captions in `assets/captions/`, and transcripts in
      `assets/transcripts/`.

## External video embeds

| Video | Used on | Publisher | Embed method | Caption status |
| ----- | ------- | --------- | ------------- | --------------- |
| [Testimony of a Genocide Survivor from Rwanda](https://www.youtube.com/watch?v=XEJ2XoIw-MM) | `index.html` "Voices of Survival" | United Nations (official channel) | Standard YouTube `iframe` embed (`youtube.com/embed/XEJ2XoIw-MM`) — not re-hosted or downloaded | Depends on the publisher's own upload; use the player's CC button. StoryCast has not independently verified caption presence/accuracy. |
| [Testimony of Béatha Mukarubuga (Maman Lambert)](https://www.youtube.com/watch?v=0aR5KogSPds) | `story/remembering-1994.html` media player | Aegis Trust (official channel) | Standard YouTube `iframe` embed (`youtube.com/embed/0aR5KogSPds`) — not re-hosted or downloaded | Same as above. |

Both titles and publisher names above were confirmed via YouTube's public
oEmbed metadata endpoint before use. Embedding via YouTube's standard
`iframe` method (rather than downloading/re-hosting the file) is the
publisher-sanctioned way to share these videos and does not require
separate permission. StoryCast has **not** produced its own transcript for
either video — see the "Transcript" section of the Story Detail page.

## Image attribution log

| File | Used on | Source | Rights status |
| ---- | ------- | ------ | -------------- |
| `assets/images/home-hero-kigali-memorial-flame.png` | `index.html` hero | Provided by the project author; found via a general web/image search, original publisher/photographer not identified | **Not confirmed.** Do not submit/publish this site with this file until a specific source and license (or the author's own photography) is confirmed. The on-page caption says "Source unconfirmed — pending rights verification before publication" for exactly this reason. If rights cannot be confirmed, replace with a Creative-Commons-licensed photo (e.g. Wikimedia Commons, properly credited) or the author's own photograph before submission. |

## Attribution requirements

- Every testimony, quotation, statistic, or media clip must be attributed to
  its verified source directly next to its use (e.g. in the References
  section of `story/remembering-1994.html`).
- Do not paraphrase testimony in a way that changes its meaning.
- Do not present unverified or placeholder text as fact — placeholder
  copy must remain clearly marked as pending research until replaced.
- Record all final attributions in the References section of the story page
  and keep a corresponding entry here once verified.
- **Never name a real, identifiable person** (e.g. a historian, journalist,
  or academic) as an advisor, reviewer, or endorser of this project unless
  that person has actually agreed to the role in writing. The "Advisory
  Council" on `about.html` lists role titles only, marked "seat unfilled,"
  for exactly this reason — see `accessibility-checklist.md` and the
  README's "Known limitations" section for the full rationale.

## Verified research notes

| Date | Topic | Source | Verified by | Notes |
| ---- | ----- | ------ | ------------ | ----- |
| 2026-10-17 | Home-page featured video | United Nations, YouTube video `XEJ2XoIw-MM`, "Testimony of a Genocide Survivor from Rwanda" | Title/publisher confirmed via YouTube's public oEmbed endpoint | Embedded via standard iframe; content of the testimony itself not independently reviewed by this project. |
| 2026-10-17 | Story Detail page testimony | Aegis Trust, YouTube video `0aR5KogSPds`, "Testimony of Béatha Mukarubuga (Maman Lambert), a survivor of the 1994 Genocide against the Tutsi" | Title/publisher confirmed via YouTube's public oEmbed endpoint | Embedded via standard iframe; biographical details beyond the published title were intentionally not added (see `accessibility-checklist.md`). |
