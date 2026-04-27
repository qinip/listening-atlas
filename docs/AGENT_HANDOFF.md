# Agent Handoff

Read this first if you are the AI agent using this repository to create a new listening atlas.

## How To Use This File

Treat this file as the entry point for the repository. If you can read local files, do not ask the user to paste a long file pack. Read the files named below when each phase needs them.

If you cannot read repository files directly, ask the user to attach `docs/AGENT_HANDOFF.md` first, then request the next phase's files only when you need them. Do not ask for the whole repository at once.

## Your Job

Create a structured music listening project from the user's brief. The required outputs are:

1. A project brief.
2. A platform-agnostic playlist TSV.
3. A Markdown listening guide.
4. A platform execution log TSV if you create or edit a playlist on a streaming service.

Optional outputs include a static HTML ebook, music-history map, chapter images, appendices, asset manifest, and release ZIPs.

## Start Here

1. Read `docs/USAGE.md`, `docs/PLAYBOOK.md`, `specs/DELIVERABLES.md`, `specs/PLAYLIST_SCHEMA.md`, and `templates/project_brief.template.md`.
2. Ask the user only for choices that materially change the project: music domain, audience, language, platform, track count, privacy, modern-music scope, screen/video inclusion, and whether the output needs an ebook or release package.
3. Fill the project brief before drafting a playlist.
4. Work through the phases below in order. Do not jump to platform execution before the source playlist TSV and recording review are coherent.
5. Keep the playlist TSV as the source of truth. Platform search results, substitutions, and unavailable tracks belong in the execution log.

## Files To Read First

Read these before generating content. If you already read them from the Start Here step, continue to Phase 1.

- `docs/USAGE.md`
- `docs/PLAYBOOK.md`
- `specs/DELIVERABLES.md`
- `specs/PLAYLIST_SCHEMA.md`
- `templates/project_brief.template.md`

If the brief describes jazz, Peking opera, a local tradition, video-first performance, or another domain that does not fit the core schema, also read:

- `specs/EXTENSION_CONTRACT.md`
- the relevant file in `specs/extensions/`

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

Do not proceed until the brief specifies music domain, language, audience, track count, platform, privacy expectation, domain fit, extension needs, and required deliverables.

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
