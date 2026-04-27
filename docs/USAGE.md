# How To Use This Repository

This file answers the practical question: if a new user wants to create their own playlist, what do they actually do with this repository?

## The Short Version

Use this repository as an instruction pack for an AI agent. You do not need to run code from it.

Give the agent the relevant docs, have it fill a project brief, then have it generate and execute a playlist plan on your chosen platform.

## Recommended File Pack For A New Project

Start by giving your agent these files:

- `docs/USAGE.md`
- `docs/AGENT_HANDOFF.md`
- `docs/PLAYBOOK.md`
- `specs/DELIVERABLES.md`
- `templates/project_brief.template.md`
- `specs/PLAYLIST_SCHEMA.md`
- `specs/PLATFORM_ADAPTERS.md`
- `prompts/01_project_brief.md`

After the brief is complete, add the next prompt for the current phase:

- Playlist drafting: `prompts/02_playlist_generation.md`
- Recording review: `prompts/03_recording_selection.md`
- Platform execution: `prompts/04_platform_execution.md`, `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md`, `templates/platform_execution_log.template.tsv`
- Guide and ebook writing: `prompts/05_guide_and_ebook.md`, `specs/GUIDE_AND_EBOOK_SPEC.md`
- Visual map, chapter art, and appendices: `prompts/07_visuals_and_appendices.md`, `specs/VISUAL_AND_APPENDIX_MODULES.md`, `specs/ASSET_MANIFEST_SPEC.md`
- Final review: `prompts/06_qa_review.md`

## One-Shot Bootstrap Prompt

If your agent can read files from a repository, start with:

```text
Read docs/USAGE.md, docs/PLAYBOOK.md, specs/DELIVERABLES.md,
specs/PLAYLIST_SCHEMA.md, specs/PLATFORM_ADAPTERS.md, and
templates/project_brief.template.md.

Create a project brief for my listening atlas. Ask only for missing
preferences that materially change the output. After the brief is settled,
produce the required deliverables in specs/DELIVERABLES.md:

1. guide Markdown
2. platform-agnostic playlist TSV
3. platform execution log TSV if you create or edit a streaming playlist

Optional features such as a music-history map, chapter images, asset manifest,
and appendices should follow specs/VISUAL_AND_APPENDIX_MODULES.md.
```

## Workflow With Codex, Claude Code, Or Similar Agents

1. Open a new agent session in a workspace where you want the new project to live.
2. Add or paste the recommended file pack.
3. Tell the agent: “Read these files and create my project brief. Ask only if a missing preference materially changes the output.”
4. Answer the agent’s questions about audience, language, music platform, track count, and scope.
5. Ask the agent to generate a playlist TSV using `specs/PLAYLIST_SCHEMA.md`.
6. Ask the agent to review recording choices using `prompts/03_recording_selection.md`.
7. If the agent has browser/computer-use access, ask it to execute the playlist on your platform using `prompts/04_platform_execution.md` and log the result with `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md`.
8. Ask the agent to write the listening guide and HTML ebook using `prompts/05_guide_and_ebook.md`.
9. Ask the agent to run `prompts/06_qa_review.md` against `docs/QUALITY_CHECKLISTS.md`.

## What The User Has To Decide

The user should decide:

- Language.
- Target audience.
- Music domain.
- Music platform.
- Track count.
- Whether to include film, game, and screen media.
- How modern the guide should be.
- Whether the output should be a private playlist, a public guide, or a release-quality ebook.

The agent can infer or recommend most other details.

## What The Agent Should Produce

A complete project should produce:

- A project brief.
- A platform-agnostic playlist TSV that follows `specs/PLAYLIST_SCHEMA.md`.
- A platform execution log TSV that follows `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md` if the playlist was created or edited on a streaming service.
- A listening guide in Markdown.
- A static HTML ebook.
- An asset manifest if images are bundled.
- A release checklist result.

For exact filenames and acceptance rules, use `specs/DELIVERABLES.md`.

## How The Existing Products Should Be Used

The files in `products/zh-CN/` and `products/en/` are examples of finished outputs. They are useful references for structure, tone, and scope.

Do not treat the Apple Music case-study fields as required. If you are using Spotify, YouTube Music, TIDAL, NetEase Cloud Music, or another platform, keep the core playlist fields and add your own platform execution notes.

## What Not To Do

- Do not ask the user to run hidden scripts from this repository.
- Do not bundle album art or artist photos copied from a music platform.
- Do not make the source playlist depend on one platform’s metadata.
- Do not skip platform verification for version-sensitive works, multi-movement works, live recordings, remasters, covers, or tracks with many similarly named versions.
