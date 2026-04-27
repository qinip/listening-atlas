# Prompt 02: Playlist Generation

Use this prompt after the project brief is settled.

```text
Using the attached project brief and playlist schema, generate a platform-agnostic music playlist draft for the requested music domain.

Requirements:

- Follow the requested track count and chapter structure.
- Keep the historical sequence readable.
- Use the chapter model from the brief. If the domain is classical, balance early music, Baroque, Classical, Romantic, modernist, postwar, minimalist, screen-media, and contemporary chapters according to the brief.
- For each row, include `row_id`, `track_no`, creator/composer/artist, work or track title, recommended recording or release, performers, search keywords, difficulty, and educational role.
- Include stable `track_no` values and stable `row_id` values.
- Include `strict_search_query`, `medium_search_query`, and `fallback_search_query` when the project will be executed on a streaming platform.
- For jazz, rock, folk, electronic music, hip-hop, and other recorded-music domains, add optional fields such as personnel, recording date, label, take/version, and source work when they are musically important.
- Include both canonical entry points and less obvious works that improve representation or explain a historical transition.
- Do not use platform-only metadata as source truth.
- Do not include album artwork or image assets.
- Mark rows that need human or platform verification.

Return the playlist as a TSV-compatible table using the schema fields. The result should be saveable as `{project_slug}_playlist.{lang}.tsv`.
```
