# Prompt 04: Platform Execution

Use this prompt with a browser/computer-use agent that can operate the selected music platform.

```text
You are executing a platform-agnostic music playlist on the selected music platform. Follow the platform adapter protocol.

Before modifying a user account, confirm the target platform, account, playlist name, privacy setting, and whether you may create or edit the playlist.

For each playlist row:

1. Search using `strict_search_query` when present.
2. If needed, try `medium_search_query` and `fallback_search_query`.
3. Confirm composer, work title, movement, performer/conductor/ensemble, album/release, and duration when visible.
4. Add one best match to the playlist.
5. Record the result using `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md`.
6. Do not download artwork, thumbnails, or platform images.
7. Do not use platform metadata to rewrite the source dataset.

If no safe match exists, mark the row unavailable and continue.

After all rows are processed, inspect the playlist order. Verify that final order follows ascending `track_no`; fix the order when possible, or record `order_status=not_visible` / `needs_human_review` with a reason.

Return:

- The platform playlist URL if public or safe to share.
- A complete platform execution log TSV.
- A short summary of exact matches, fallbacks, unavailable rows, duplicates, and order-verification status.
```
