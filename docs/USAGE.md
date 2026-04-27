# How To Use This Repository

This file answers the practical question: if a new user wants to create their own playlist, what do they actually do with this repository?

## The Short Version

Use this repository as an instruction pack for an AI agent. You do not need to run code from it.

If your agent can read files from a cloned repository, point it to `docs/AGENT_HANDOFF.md` first. That file is the entry point. The agent should read the other docs, specs, templates, and prompts as each phase needs them.

## One-File Bootstrap Prompt

Use this when your agent has access to the repository:

```text
Read docs/AGENT_HANDOFF.md first and use it as the entry point for this repository.
Help me create a music listening guide, playlist TSV, and platform playlist for [genre or domain].
Target platform: [Apple Music / Spotify / YouTube Music / YouTube / TIDAL / NetEase Cloud Music / other].
Target size: about [50 / 100 / 180] tracks.
Language: [English / Chinese / other].
Ask me for any missing project-brief choices, then follow the kit.
```

## If Your Agent Cannot Read The Repository

Some chat agents cannot browse a local repository or follow relative file paths. In that case, attach `docs/AGENT_HANDOFF.md` first, then attach the files it asks for phase by phase. For the first phase, the minimum useful pack is:

- `docs/USAGE.md`
- `docs/AGENT_HANDOFF.md`
- `docs/PLAYBOOK.md`
- `specs/DELIVERABLES.md`
- `templates/project_brief.template.md`
- `specs/PLAYLIST_SCHEMA.md`
- `specs/PLATFORM_ADAPTERS.md`
- `prompts/01_project_brief.md`

If your domain does not fit the classical demo model, also give the agent:

- `specs/EXTENSION_CONTRACT.md`
- any relevant file in `specs/extensions/`

After the brief is complete, add the next prompt for the current phase:

- Playlist drafting: `prompts/02_playlist_generation.md`
- Recording review: `prompts/03_recording_selection.md`
- Platform execution: `prompts/04_platform_execution.md`, `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md`, `templates/platform_execution_log.template.tsv`
- Guide and ebook writing: `prompts/05_guide_and_ebook.md`, `specs/GUIDE_AND_EBOOK_SPEC.md`
- Visual map, chapter art, and appendices: `prompts/07_visuals_and_appendices.md`, `specs/VISUAL_AND_APPENDIX_MODULES.md`, `specs/ASSET_MANIFEST_SPEC.md`
- Final review: `prompts/06_qa_review.md`

## Workflow With Codex, Claude Code, Or Similar Agents

1. Open a new agent session in a workspace where you want the new project to live.
2. Clone or download this repository into that workspace, or attach `docs/AGENT_HANDOFF.md` if the agent cannot read local files.
3. Tell the agent to read `docs/AGENT_HANDOFF.md`, create the project brief, and ask only if a missing preference materially changes the output.
4. Answer the agent’s questions about audience, language, music platform, track count, and scope.
5. If the domain fit worksheet shows gaps, ask the agent to select or draft a domain extension before generating the playlist.
6. Ask the agent to generate a playlist TSV using `specs/PLAYLIST_SCHEMA.md` plus any selected extension.
7. Ask the agent to review recording choices using `prompts/03_recording_selection.md`.
8. If the agent has browser/computer-use access, ask it to execute the playlist on your platform using `prompts/04_platform_execution.md` and log the result with `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md`.
9. Ask the agent to write the listening guide and HTML ebook using `prompts/05_guide_and_ebook.md`.
10. Ask the agent to run `prompts/06_qa_review.md` against `docs/QUALITY_CHECKLISTS.md`.

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
- A QA review result against `docs/QUALITY_CHECKLISTS.md`.

For exact filenames and acceptance rules, use `specs/DELIVERABLES.md`.

## How The Existing Products Should Be Used

The files in `products/zh-CN/` and `products/en/` are examples of finished outputs. They are useful references for structure, tone, and scope.

Do not treat the Apple Music case-study fields as required. If you are using Spotify, YouTube Music, TIDAL, NetEase Cloud Music, or another platform, keep the core playlist fields and add your own platform execution notes.

The release ZIPs attached to GitHub Releases are demo products for Classical Atlas. To use the agent kit, clone or download the repository and read the docs/specs/prompts/templates rather than starting from the ZIP alone.

## What Not To Do

- Do not ask the user to run hidden scripts from this repository.
- Do not bundle album art or artist photos copied from a music platform.
- Do not make the source playlist depend on one platform’s metadata.
- Do not skip platform verification for version-sensitive works, multi-movement works, live recordings, remasters, covers, or tracks with many similarly named versions.
