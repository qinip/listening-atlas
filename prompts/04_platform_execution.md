# Prompt 04: Platform Execution

Use this prompt with a browser/computer-use agent that can operate the selected music platform.

```text
You are executing a platform-agnostic classical music playlist on the selected music platform. Follow the platform adapter protocol.

For each playlist row:

1. Search using the strict query.
2. If needed, try the medium and fallback queries.
3. Confirm composer, work title, movement, performer/conductor/ensemble, album/release, and duration when visible.
4. Add one best match to the playlist.
5. Record track_no, platform, platform_query, selected result title, selected result URL if available, match status, and reason.
6. Do not download artwork, thumbnails, or platform images.
7. Do not use platform metadata to rewrite the source dataset.

If no safe match exists, mark the row unavailable and continue.
```

