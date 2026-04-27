# Prompt 05: Guide And Ebook

Use this prompt after the playlist has been reviewed.

```text
Write a music listening guide from the playlist and project brief.

Requirements:

- Explain the editorial premise.
- Write chapter introductions that explain historical context, listening method, influence chain, and entry works.
- Tie every chapter's entry works back to the playlist TSV using `track_no` or `row_id`.
- Include a composer index and pronunciation notes when available.
- Include concise fun fact boxes where they clarify the material.
- Add appendices for work catalog numbers, comparing recordings, and glossary terms.
- Keep the guide accessible to beginners without oversimplifying.
- Do not rely on album covers or platform images.
- If preparing static HTML, include a timeline/tree insert using static HTML/CSS or a separately licensed image with asset manifest.
- If adding chapter images, maps, platform links, or appendices, follow `specs/VISUAL_AND_APPENDIX_MODULES.md`.
- Keep all visual asset placeholders tied to the asset manifest.
- For multilingual releases, produce separate language editions rather than interleaving translations in one document.

Return:

- A Markdown guide saveable as `{project_slug}_guide.{lang}.md`.
- A static HTML publishing plan, or the HTML itself if requested.
- An asset manifest draft if images are bundled or generated.
```
