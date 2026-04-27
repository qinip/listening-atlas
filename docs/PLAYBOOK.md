# Playbook

This playbook explains how to use a browser/computer-use AI agent to create a structured music playlist, listening guide, and static HTML ebook without binding the method to one music platform. The current reference product is classical, but the workflow can be adapted to other music domains.

## 0. Deliverable Contract

Before generating content, read `specs/DELIVERABLES.md`.

The hard deliverables are:

- A completed project brief.
- A platform-agnostic source playlist TSV.
- A Markdown listening guide.
- A platform execution log TSV if the agent creates or edits a streaming playlist.

Optional deliverables include a static HTML ebook, music-history map, chapter images, appendices, asset manifest, and release ZIPs.

## 1. Define The Brief

Start from `templates/project_brief.template.md`. The brief must settle:

- Music domain, such as classical, jazz, rock, film music, game music, or a local tradition.
- Audience and assumed listening background.
- Output language.
- Target music platform or manual execution mode.
- Track count.
- Historical scope.
- Post-1900 proportion.
- Basic/advanced split.
- Whether film, game, screen media, and cross-genre music are in scope.
- Ebook target: Markdown only, static HTML, or static HTML plus later EPUB.
- Asset policy and release criteria.

## 2. Build The Historical Frame

Use a chronological backbone, then add topical chapters only when they explain modern listening paths.

For a classical atlas, this chapter model works well:

1. Early music and polyphony
2. Baroque
3. Classical period
4. Romanticism and national styles
5. Early modernism
6. Interwar modernism, jazz, Soviet context, and recording media
7. Postwar avant-garde and sound experiments
8. Minimalism and post-minimalism
9. Film, game, and screen media music
10. Contemporary classical and cross-genre composition after 1990

For another domain, keep the same editorial logic but replace the chapter model with a domain-specific timeline, geography, scene, label, technology, or subgenre structure.

## 3. Create The Candidate Universe

For each chapter, ask the agent to propose:

- 10 to 30 representative composers or traditions.
- 1 to 3 candidate works per composer.
- A short reason why each work belongs in the chapter.
- A basic or advanced difficulty label.
- Whether the work explains a historical transition, listening technique, medium shift, or instrumentation.

The candidate universe should be larger than the final playlist. A 180-track guide may start from 300 to 500 candidates.

## 4. Select Works

Apply these rules:

- Keep the sequence historically readable.
- Avoid choosing only the most famous excerpt when another work explains the chapter better.
- Include vocal and instrumental traditions.
- Include opera, chamber music, sacred music, keyboard music, symphonic music, film, game, and contemporary forms when they serve the educational goal.
- Prefer one strong entry point per concept over many similar works.
- Track gaps by era, region, gender, race, medium, and instrumentation.

## 5. Select Recordings

Classical music search is version-sensitive. A good row identifies both the work and the recommended recording.

For each selected work:

- Record composer, work title, recommended album or release, performers, conductor, ensemble, and useful catalog numbers.
- Generate strict, medium, and fallback search strings.
- Prefer recordings that are available on the target platform and easy for beginners to identify.
- Provide a fallback version for historically important recordings that may be hard to find.
- Never assume that the first search result is correct.

## 6. Execute On The Platform

Use `specs/PLATFORM_ADAPTERS.md` and `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md`. The execution agent should:

- Search one row at a time.
- Confirm title, composer, movement, performers, album, and duration when available.
- Add the best match to the playlist.
- Record mismatches, unavailable tracks, duplicate adds, and fallback choices.
- Verify final playlist order against ascending `track_no`.
- Keep platform execution notes separate from the source dataset.

## 7. Write The Guide

The guide should explain how to listen, not only what to hear.

Each chapter should include:

- Historical setting.
- Listening technique.
- Influence chain.
- Entry-point works.
- Terms that matter in this chapter.
- Optional fun fact or listening-tip box.

## 8. Publish The Ebook

Static HTML is the first publishing target. EPUB can be generated later from the same structured content.

Requirements:

- No JavaScript required.
- Responsive typography.
- A timeline or tree insert mapping eras, regions, genres, composers, and works.
- Text boxes for fun facts and listening tips.
- Asset manifest for every packaged visual.
- Clear separation between source links and bundled assets.

If the project asks for a richer ebook, use `specs/VISUAL_AND_APPENDIX_MODULES.md` for:

- A music-history map.
- Chapter opener images.
- Composer, catalog-number, recording-comparison, and glossary appendices.
- Platform playback or search links derived from the execution log.

## 9. Package The Finished Products

Keep finished products separate from source instructions:

- `products/zh-CN/`: Chinese guide, playlist, and ebook files.
- `products/en/`: English guide, playlist, and ebook files.
- `release-assets/`: ZIP files to upload to a GitHub Release.
- `site/`: GitHub Pages static HTML with language-switch links.

## 10. Review And Release

Before release:

- Run `docs/QUALITY_CHECKLISTS.md`.
- Confirm no automation scripts are included.
- Confirm all bundled visuals are listed in an asset manifest.
- Confirm sample output is labeled as a case study.
- Confirm platform-specific instructions are advisory, not dependencies.
