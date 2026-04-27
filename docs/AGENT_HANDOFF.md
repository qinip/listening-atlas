# Agent Handoff

Read this first if you are the AI agent using this repository to create a new listening atlas.

## Your Job

Create a structured music listening project from the user's brief. The required outputs are:

1. A project brief.
2. A platform-agnostic playlist TSV.
3. A Markdown listening guide.
4. A platform execution log TSV if you create or edit a playlist on a streaming service.

Optional outputs include a static HTML ebook, music-history map, chapter images, appendices, asset manifest, and release ZIPs.

## Files To Read First

Read these before generating content:

- `docs/USAGE.md`
- `docs/PLAYBOOK.md`
- `specs/DELIVERABLES.md`
- `specs/PLAYLIST_SCHEMA.md`
- `templates/project_brief.template.md`

If you will create or edit a playlist on a streaming service, also read:

- `specs/PLATFORM_ADAPTERS.md`
- `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md`
- `templates/platform_execution_log.template.tsv`
- `prompts/04_platform_execution.md`

If you will create an ebook with visuals or appendices, also read:

- `specs/GUIDE_AND_EBOOK_SPEC.md`
- `specs/VISUAL_AND_APPENDIX_MODULES.md`
- `specs/ASSET_MANIFEST_SPEC.md`
- `templates/asset_manifest.template.tsv`
- `templates/music_history_map_nodes.template.tsv`

## Work Phases

### Phase 1: Project Brief

Use `prompts/01_project_brief.md`.

Output:

- `{project_slug}_brief.md`

Do not proceed until the brief specifies music domain, language, audience, track count, platform, privacy expectation, and required deliverables.

### Phase 2: Playlist Source TSV

Use `prompts/02_playlist_generation.md` and `specs/PLAYLIST_SCHEMA.md`.

Output:

- `{project_slug}_playlist.{lang}.tsv`

The TSV is the source of truth. Keep it platform-agnostic. Use stable `track_no` order and stable `row_id` values.

### Phase 3: Recording Review

Use `prompts/03_recording_selection.md`.

Output:

- `{project_slug}_recording_review.{lang}.tsv` or review notes added to the source TSV.

Fix ambiguous titles, weak performer metadata, missing fallback recordings, and weak search queries before platform execution.

### Phase 4: Platform Execution

Use `prompts/04_platform_execution.md`.

Output:

- `{project_slug}_{platform}_execution_log.{lang}.tsv`

Before changing a user's streaming account, confirm platform, account, playlist name, privacy setting, and permission to create or edit the playlist.

Add or mark every source row. Do not silently skip rows. Verify final order against `track_no`.

### Phase 5: Guide Markdown

Use `prompts/05_guide_and_ebook.md` and `specs/GUIDE_AND_EBOOK_SPEC.md`.

Output:

- `{project_slug}_guide.{lang}.md`

The guide must cite entry works by `track_no` or `row_id`. It should explain how to listen, not only list works.

### Phase 6: Optional Ebook, Visuals, And Appendices

Use `prompts/07_visuals_and_appendices.md` when requested.

Outputs may include:

- `{project_slug}_guide.{lang}.html`
- `assets/ASSET_MANIFEST.tsv`
- music-history map data or static map markup
- chapter image plan
- appendices tied to playlist rows

Every bundled image must be in the asset manifest before release.

### Phase 7: QA

Use `prompts/06_qa_review.md` and `docs/QUALITY_CHECKLISTS.md`.

Return:

- Blocking issues.
- Non-blocking improvements.
- Release notes.
- Publish / no-publish recommendation.

## Hard Rules

- Do not run or invent automation scripts from this repository.
- Do not bundle platform album art, thumbnails, screenshots, comments, cookies, credentials, or browser profiles.
- Do not let platform metadata overwrite the source playlist TSV.
- Do not publish private playlist links or account-specific URLs.
- Do not claim that a streaming playlist is complete unless the execution log covers every source row and order has been checked or explicitly marked unavailable to verify.
