# Prompt 07: Visuals And Appendices

Use this prompt only when the project brief asks for a richer ebook with a music-history map, chapter images, platform links, or expanded appendices.

```text
Using the project brief, playlist TSV, guide draft, asset manifest spec, and
visual/appendix module spec, design the optional visual and appendix layer.

Requirements:

- Propose a music-history map that uses a limited set of representative eras,
  composers, genres, media, and works. It does not need to include every row.
- Return map data using `templates/music_history_map_nodes.template.tsv`, or
  explain why a static text/HTML map is enough.
- For each chapter image, explain why the image fits the chapter's topic.
- Use only public domain, CC0, compatible CC assets, or self-generated visuals
  allowed by the project brief.
- Add every bundled image to `ASSET_MANIFEST.tsv`.
- Do not use platform album art, thumbnails, artist photos, or screenshots as
  bundled assets unless a separate reusable license is documented.
- Build appendices that point back to playlist `track_no` or `row_id` values.
- If platform links are included, derive them from the platform execution log
  and label them by platform.

Return:

- Map node data or a static map plan.
- Chapter image plan with asset IDs.
- Appendix plan with playlist row references.
- Asset manifest additions.
- Any blocking license or source gaps.
```
