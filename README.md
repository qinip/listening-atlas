# Listening Atlas Agent Kit

A documentation-first toolkit for using browser/computer-use AI agents to create structured music playlists, listening guides, and static ebook releases on any music platform. The included reference product is `Classical Atlas`.

中文说明见 [README.zh-CN.md](README.zh-CN.md).

## What This Repository Is

This repository is not an automation-code project. It is an agent kit: a set of prompts, specs, checklists, templates, and sample outputs that a user can hand to Codex, Claude Code, or another browser/computer-use agent.

The goal is platform independence. A user should be able to create a playlist and guide for Apple Music, Spotify, YouTube Music, YouTube, TIDAL, NetEase Cloud Music, or another platform without changing the editorial method.

## What Is Included

- `docs/`: the workflow and QA checklists.
- `specs/`: deliverable contract, schemas, platform protocol, visual modules, and publishing requirements.
- `specs/extensions/`: optional domain-extension stubs for fields and platform rules that do not belong in the core schema.
- `prompts/`: copy-ready prompts for agents.
- `templates/`: project brief, playlist row, and asset manifest templates.
- `products/zh-CN/`: the Chinese finished guide and playlist.
- `products/en/`: the English finished guide and playlist.
- `site/`: static GitHub Pages ebook prototype with a language switch.
- `samples/`: original Apple Music case-study material.
- `DEMO_RELEASE_NOTES.md`: copy-ready GitHub Release text explaining that attached ZIPs are demo products.
- GitHub Releases: downloadable ZIP files for the finished Chinese and English products.

## Quick Start

If you want to make your own playlist:

1. Download or clone this repository.
2. Give your agent these files:
   - `docs/USAGE.md`
   - `docs/AGENT_HANDOFF.md`
   - `docs/PLAYBOOK.md`
   - `specs/DELIVERABLES.md`
   - `templates/project_brief.template.md`
   - `specs/PLAYLIST_SCHEMA.md`
   - `specs/PLATFORM_ADAPTERS.md`
   - the relevant prompt from `prompts/`
   - `specs/EXTENSION_CONTRACT.md` and `specs/extensions/*` when your domain needs extra fields or video/archive handling
3. Ask the agent to fill the project brief for your audience, language, platform, and track count.
4. Ask the agent to generate a platform-agnostic playlist TSV.
5. Ask a browser/computer-use agent to execute the TSV on your chosen music platform.
6. Ask the agent to write the guide and static HTML ebook.
7. Run the QA checklists before publishing.

For detailed instructions, read [docs/USAGE.md](docs/USAGE.md).

## Finished Products

The repository contains two independent finished products:

- Chinese: `products/zh-CN/classical_atlas_guide.zh-CN.md` and `products/zh-CN/classical_atlas_playlist.zh-CN.tsv`
- English: `products/en/classical_atlas_guide.en.md` and `products/en/classical_atlas_playlist.en.tsv`

These products are the Apple Music edition of the Classical Atlas demo. Apple Music search columns, package prompts, and reconstructed execution logs are case-study material; the reusable platform-agnostic contract lives in `specs/`, `prompts/`, and `templates/`.

GitHub Release ZIP files are downloadable **demo product artifacts**, not the primary agent kit deliverable. The reusable kit is the repository itself: `docs/`, `specs/`, `prompts/`, and `templates/`. `site/downloads/` contains committed demo ZIP copies for GitHub Pages links. Local build output may be staged in `release-assets/`, but that directory is not committed and is not the source of truth.

## GitHub Pages

The `site/` directory contains a static HTML ebook prototype:

- `site/index.html`: Chinese edition
- `site/en/index.html`: English edition

Each page has a top-right language switch. To publish on GitHub Pages, either deploy `site/` with a Pages workflow or copy the contents of `site/` to the branch/folder your repository already uses for Pages.

## Asset Policy

This project uses a conservative open-publishing policy:

- Bundled images must be public domain, CC0, or clearly reusable under a compatible open license.
- Wikimedia Commons files require file-level license, author, source, and attribution checks.
- The Met Open Access / CC0 is preferred for public-domain art images.
- Platform-provided album art, artist photos, thumbnails, and metadata from Spotify, TIDAL, Apple Music, YouTube, or NetEase Cloud Music should be linked or generated locally by the user, not bundled here.
- Every bundled visual asset must appear in an asset manifest.

## License

Reusable kit materials in `docs/`, `specs/`, `prompts/`, and `templates/` are dedicated under [CC0 1.0](LICENSE.md). Finished demo products, sample guide text, sample playlist data, and site guide content are licensed under [CC BY 4.0](LICENSE.md), unless otherwise noted.

Third-party sources keep their own licenses and terms. This repository does not provide legal advice.
