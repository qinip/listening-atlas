# Guide And Ebook Spec

The guide is the explanation layer for the playlist. The ebook is the publishable reading layer.

## Guide Structure

Required sections:

1. Title and editorial premise.
2. How to use the playlist.
3. Composer index and pronunciation notes when available.
4. Chapter-by-chapter listening guide.
5. Appendix on work catalog numbers.
6. Appendix on comparing recordings.
7. Glossary.
8. References and source notes.

## Chapter Template

Each chapter should include:

- Historical context: what changed in institutions, instruments, notation, recording, or listening habits.
- Listening method: what a beginner should notice first.
- Influence chain: how this chapter connects to earlier and later music.
- Entry works: 3 to 6 suggested starting points.
- Fun fact or side note: optional, short, and visually distinct in ebook form.

## Static HTML Ebook

HTML is the first release target because it supports visual layout, internal links, responsive typography, and static tree diagrams without platform dependencies.

Requirements:

- Single static HTML file or a small static folder.
- No JavaScript required.
- No external tracking, analytics, or platform SDKs.
- CSS may be embedded.
- Must remain readable offline if packaged assets are present.
- All bundled images must be listed in an asset manifest.
- If an image is only linked from a source page, label it as external and do not imply it is bundled.
- A top-right language switch should link the Chinese and English editions.

## Visual System

Use restrained editorial design:

- Serif or humanist body text.
- Clear chapter openers.
- Side boxes for listening tips, fun facts, and source notes.
- A timeline or tree insert for eras, regions, genres, composers, and works.
- Color accents that distinguish note types without overwhelming the reading experience.
- Do not rely on album covers as decoration.

## GitHub Pages Layout

Recommended static structure:

- `site/index.html`: Chinese edition.
- `site/en/index.html`: English edition.
- `site/assets/`: only reviewed local assets.

Each page should include:

- A top-right language switch.
- Links to the Chinese and English release ZIP files.
- A note that platform artwork is not bundled.

## EPUB Later

EPUB should be treated as an export target after the HTML structure is stable.

Before EPUB export:

- Reduce layout dependence on complex CSS.
- Confirm all images are local and licensed.
- Add a proper table of contents.
- Test on at least Apple Books and Calibre.

