# Deliverables Contract

This contract defines what a successful Listening Atlas project must produce. It is written for a second AI agent that has no private context from the original project.

## Required Deliverables

Use a stable project slug such as `classical_atlas`, `jazz_atlas`, or `film_music_atlas`.

| Deliverable | Suggested filename | Required | Purpose |
| --- | --- | --- | --- |
| Project brief | `{project_slug}_brief.md` | yes | Freezes audience, language, platform, track count, scope, ratios, and asset policy. |
| Source playlist TSV | `{project_slug}_playlist.{lang}.tsv` | yes | Platform-agnostic source of truth for all tracks and order. |
| Recording review notes | `{project_slug}_recording_review.{lang}.tsv` | recommended | Flags ambiguous works, weak metadata, fallback recordings, and search risks before platform execution. |
| Platform execution log | `{project_slug}_{platform}_execution_log.{lang}.tsv` | yes if a playlist is created on a platform | Records what was actually searched, selected, added, skipped, substituted, and order-verified. |
| Guide Markdown | `{project_slug}_guide.{lang}.md` | yes | The publishable listening guide linked to playlist rows. |
| Static HTML ebook | `{project_slug}_guide.{lang}.html` or `site/index.html` | recommended | Readable, shareable version of the guide. |
| Asset manifest | `assets/ASSET_MANIFEST.tsv` | required if any image is bundled | License and attribution ledger for portraits, artworks, chapter images, and diagrams. |
| Release notes | `{project_slug}_release_notes.md` | recommended | Explains what is included, what platform was used, and known limitations. |

## Source Of Truth Rules

- The source playlist TSV owns sequence, work identity, chapter membership, and educational role.
- The platform execution log owns platform-specific results, URLs, substitutions, unavailable rows, and final order verification.
- The guide must cite playlist rows by `track_no` or a stable row identifier when it recommends entry works.
- The asset manifest owns all bundled visual-asset rights and attribution metadata.
- Platform artwork, thumbnails, comments, user account data, cookies, screenshots, or private URLs must not become source truth.

## Minimum Viable Output

A minimal successful run produces:

1. A completed project brief.
2. A valid source playlist TSV with stable `track_no` order.
3. A Markdown guide with chapter sections and entry works tied to source rows.
4. A platform execution log showing whether each row was added, substituted, unavailable, or rejected.

Static HTML, visual maps, chapter art, pronunciation appendices, and release ZIPs are valuable but optional unless requested in the brief.

## Definition Of Done

Before release, the agent must be able to answer yes to all of these:

- Can another agent open only this kit plus the project files and reproduce the playlist shape?
- Does every playlist row have enough metadata to search outside the original platform?
- Does the platform execution log have one row per source playlist row?
- Does the final playlist order match ascending `track_no`, with exceptions explicitly logged?
- Does the guide explain how to listen rather than only listing pieces?
- Are all bundled visuals present in `ASSET_MANIFEST.tsv`?
- Is there no platform automation code, credential, cookie, local browser profile, or unlicensed platform media in the release?
