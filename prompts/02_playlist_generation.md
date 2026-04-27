# Prompt 02: Playlist Generation

Use this prompt after the project brief is settled.

```text
Using the attached project brief and playlist schema, generate a platform-agnostic music playlist draft for the requested music domain.

Requirements:

- Follow the requested track count and chapter structure.
- Keep the historical sequence readable.
- Use the chapter model from the brief. If the domain is classical, balance early music, Baroque, Classical, Romantic, modernist, postwar, minimalist, screen-media, and contemporary chapters according to the brief.
- For each row, include creator/composer/artist, work or track title, recommended recording or release, performers, search keywords, difficulty, and educational role.
- Include stable `track_no` values and, when possible, `row_id` values.
- Include strict, medium, and fallback search queries when the project will be executed on a streaming platform.
- Include both canonical entry points and less obvious works that improve representation or explain a historical transition.
- Do not use platform-only metadata as source truth.
- Do not include album artwork or image assets.
- Mark rows that need human or platform verification.

Return the playlist as a TSV-compatible table using the schema fields. The result should be saveable as `{project_slug}_playlist.{lang}.tsv`.
```
