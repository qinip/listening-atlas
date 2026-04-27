# Classical Music Agent Kit

A documentation-first toolkit for using browser/computer-use AI agents to create classical music playlists, listening guides, and static ebook releases on any music platform.

中文说明见 [README.zh-CN.md](README.zh-CN.md).

## What This Repository Is

This repository is not an automation-code project. It is an agent kit: a set of prompts, specs, checklists, templates, and sample outputs that a user can hand to Codex, Claude Code, or another browser/computer-use agent.

The goal is platform independence. A user should be able to create a playlist and guide for Apple Music, Spotify, YouTube Music, YouTube, TIDAL, NetEase Cloud Music, or another platform without changing the editorial method.

## What Is Included

- `docs/`: the workflow and QA checklists.
- `specs/`: schemas and publishing requirements.
- `prompts/`: copy-ready prompts for agents.
- `templates/`: project brief, playlist row, and asset manifest templates.
- `products/zh-CN/`: the Chinese finished guide and playlist.
- `products/en/`: the English finished guide and playlist.
- `site/`: static GitHub Pages ebook prototype with a language switch.
- `samples/`: original Apple Music case-study material.
- `release-assets/`: generated ZIP files intended for GitHub Releases.

## Quick Start

If you want to make your own playlist:

1. Download or clone this repository.
2. Give your agent these files:
   - `docs/USAGE.md`
   - `docs/PLAYBOOK.md`
   - `templates/project_brief.template.md`
   - `specs/PLAYLIST_SCHEMA.md`
   - `specs/PLATFORM_ADAPTERS.md`
   - the relevant prompt from `prompts/`
3. Ask the agent to fill the project brief for your audience, language, platform, and track count.
4. Ask the agent to generate a platform-agnostic playlist TSV.
5. Ask a browser/computer-use agent to execute the TSV on your chosen music platform.
6. Ask the agent to write the guide and static HTML ebook.
7. Run the QA checklists before publishing.

For detailed instructions, read [docs/USAGE.md](docs/USAGE.md).

## Finished Products

The repository contains two independent finished products:

- Chinese: `products/zh-CN/classical_music_intro_guide.zh-CN.md` and `products/zh-CN/classical_music_intro_playlist.zh-CN.tsv`
- English: `products/en/classical_music_intro_guide.en.md` and `products/en/classical_music_intro_playlist.en.tsv`

The release ZIP files are:

- `release-assets/classical-music-intro-zh-CN.zip`
- `release-assets/classical-music-intro-en.zip`

These ZIP files are meant to be uploaded to a GitHub Release page as downloadable product artifacts.

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

Original documentation, prompts, specs, templates, sample data, and generated guide text in this repository are licensed under [CC BY 4.0](LICENSE.md), unless otherwise noted.

Third-party sources keep their own licenses and terms. This repository does not provide legal advice.
