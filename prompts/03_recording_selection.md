# Prompt 03: Recording Selection

Use this prompt to improve recommended recordings before platform execution.

```text
Review the playlist rows as a music editor with domain expertise. For each row:

- Confirm whether the selected work is a good entry point for the chapter.
- Check whether the recommended recording is identifiable by performer, conductor, ensemble, release, or catalog number.
- Add a fallback recording when the preferred recording is historically important but may be hard to find.
- Improve `search_keywords`, `strict_search_query`, `medium_search_query`, and `fallback_search_query` for platform execution.
- Flag rows where the work title is ambiguous, the movement is unclear, or the performer metadata is insufficient.
- Preserve the source row fields; add review notes instead of overwriting uncertain information.

Do not optimize only for popularity. Optimize for educational clarity, availability, and version identifiability.
```
