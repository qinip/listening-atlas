# Asset Manifest Spec

The asset manifest is mandatory for any bundled image, illustration, diagram, portrait, artwork, concert photo, or album-related visual.

## Policy

Default allowed:

- Public domain assets.
- CC0 assets.
- CC BY assets with correct attribution.
- CC BY-SA assets only if the derivative and surrounding release can satisfy ShareAlike obligations.
- Self-created diagrams and generated visuals when rights are clear.

Default not allowed:

- Platform album art copied from Spotify, Apple Music, TIDAL, YouTube, YouTube Music, or NetEase Cloud Music.
- Artist photos copied from music platforms or agency pages.
- Concert photos without explicit reusable license.
- Fair-use-only assets in the open release.
- Images without source, creator, license, or reuse notes.

## Manifest Fields

Use `templates/asset_manifest.template.tsv`.

| Field | Required | Description |
| --- | --- | --- |
| `asset_id` | yes | Stable local identifier. |
| `intended_use` | yes | Portrait, artwork, chapter opener, tree diagram, fun fact box, etc. |
| `local_path` | yes if bundled | Path in the release, or `external-only`. |
| `source_url` | yes | Original source page, not only image file URL. |
| `creator` | yes | Author, artist, photographer, institution, or unknown if the source says so. |
| `title` | yes | Asset or artwork title. |
| `license` | yes | CC0, public domain, CC BY 4.0, etc. |
| `license_url` | yes unless public domain source has no URL | License link. |
| `attribution_text` | yes when attribution is required | Credit line for ebook. |
| `modifications` | yes | Cropped, resized, color-adjusted, none, etc. |
| `reuse_notes` | yes | Why it is safe enough for this release. |
| `reviewed_by` | yes | Person or agent that checked it. |
| `review_date` | yes | ISO date. |

## Source Guidance

- Wikimedia Commons: check each file page. Commons content may have different attribution, license-linking, and derivative-license requirements.
- The Met Open Access: preferred for public-domain art because Open Access images and data are available under CC0.
- Library and museum collections: use only when the item-level rights statement allows reuse.
- MusicBrainz Cover Art Archive: useful for metadata and discovery, but covers are archival and should not be treated as automatically open-licensed artwork.
- Platform developer artwork: follow platform terms and do not bundle unless you have a separate license.

## Review Rule

If the reviewer cannot explain why an asset is reusable in one sentence, do not bundle it.

