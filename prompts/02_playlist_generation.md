# Prompt 02: Playlist Generation

Use this prompt after the project brief is settled.

```text
Using the attached project brief and playlist schema, generate a platform-agnostic classical music playlist draft.

Requirements:

- Follow the requested track count and chapter structure.
- Keep the historical sequence readable.
- Balance early music, Baroque, Classical, Romantic, modernist, postwar, minimalist, screen-media, and contemporary chapters according to the brief.
- For each row, include composer, work, recommended recording, performers, search keywords, difficulty, and educational role.
- Include both canonical entry points and less obvious works that improve representation or explain a historical transition.
- Do not use platform-only metadata as source truth.
- Do not include album artwork or image assets.
- Mark rows that need human or platform verification.

Return the playlist as a TSV-compatible table using the schema fields.
```

