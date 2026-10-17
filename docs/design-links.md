# StoryCast — Design Links

## Figma wireframe

- Status: **Not available as a link.** No Figma file link was shared.
- Link: _TODO — add the Figma wireframe link here if/when it is shared._

## Figma high-fidelity mockup

- Status: **Referenced via screenshots, not a live link.** Three annotated
  screenshots (Home, Story Detail, About & Accessibility) were shared
  directly in the project chat and used as the visual reference for this
  implementation. No Figma file URL was provided.
- Link: _TODO — add the live Figma mockup link here if/when it is shared._

## What was implemented from the screenshots

Layout, section order, color palette, typography pairing (serif headings /
sans body), spacing rhythm, card and button styles, and the overall
archive/museum visual language were reproduced closely from the screenshots.

A handful of specific pieces of **content** shown in the screenshots were
deliberately **not** reproduced verbatim, because they would have meant
inventing historical testimony, fabricating verified-compliance claims, or
naming real historians/advisors without their knowledge or consent. These
are documented in detail in
[`accessibility-checklist.md`](./accessibility-checklist.md) and the
"Known limitations & deviations from the Figma screenshots" section of the
root [`README.md`](../README.md). In every case the surrounding layout,
component, and styling were kept; only the specific unverifiable facts were
replaced with honest, clearly-labeled placeholders.

## Integration plan (if a live Figma link is shared later)

1. Compare the live file against the screenshots already implemented and
   note any differences.
2. Update design tokens in `sass/_colors.scss` and `sass/_typography.scss`
   if the live file specifies different values than what was inferred from
   the screenshots.
3. Replace placeholder images/media once real, rights-cleared assets exist
   (see the checklist in [`research-notes.md`](./research-notes.md)).
4. Re-run the accessibility checklist in
   [`accessibility-checklist.md`](./accessibility-checklist.md).
