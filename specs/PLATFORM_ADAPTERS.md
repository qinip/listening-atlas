# Platform Adapters

This file describes how a computer-use agent should execute the same playlist spec on different music platforms. It is a protocol, not code.

## Shared Execution Protocol

For every platform:

1. Read one playlist row.
2. Search with `composer + work + key performer`.
3. If the result is noisy, search `composer + catalog_number + work keyword`.
4. Confirm title, composer, movement, performer, conductor, ensemble, album/release, and duration when visible.
5. Add only one best match.
6. Record match status: exact, acceptable, fallback, unavailable, duplicate, or rejected.
7. Keep platform URLs or screenshots as local execution notes, not as source truth.
8. Do not download or package platform artwork.

## Apple Music / Apple Music Classical

Strengths:

- Apple Music Classical often has richer classical metadata.
- Searching by composer, work, performer, and catalog number usually works well.

Risks:

- Apple Music and Apple Music Classical can expose different surfaces.
- Search may pick a different movement from the same work.
- Some add-to-playlist actions may silently fail or duplicate.

Agent instructions:

- Prefer Apple Music Classical search when available.
- Search work pages before album pages when possible.
- Verify movement title for multi-movement works.
- Record exact query and selected result.

## Spotify

Strengths:

- Broad catalog and stable sharing links.
- Playlists are easy to create and share.

Risks:

- Classical work metadata is inconsistent.
- Spotify artwork and metadata must follow Spotify attribution and linking requirements.
- Spotify artwork should not be treated as reusable ebook imagery.

Agent instructions:

- Use composer plus performer plus catalog number.
- Prefer the exact movement title over the most popular result.
- Preserve Spotify URLs as platform execution links.
- Do not download or package album artwork.

## YouTube Music

Strengths:

- Wide availability and many recordings.
- Useful fallback when subscription catalogs differ by region.

Risks:

- Official tracks, auto-generated tracks, live videos, and user uploads may mix together.
- Titles can be noisy.
- Video thumbnails are not reusable assets.

Agent instructions:

- Prefer official artist, channel, or release entries when available.
- Reject low-quality uploads unless the brief explicitly allows archival videos.
- Record whether the result is audio release, official video, live performance, or user upload.

## YouTube

Strengths:

- Good for public lectures, performances, historical recordings, and unavailable works.
- Useful for educational guides.

Risks:

- Rights and upload quality vary widely.
- Comments, thumbnails, and visual content can distract from the listening goal.
- Not every video is legal or stable.

Agent instructions:

- Prefer official orchestra, opera house, label, artist, museum, or composer-estate channels.
- Use YouTube as a fallback or supplement unless the project brief makes it the primary platform.
- Document source channel and reason for acceptance.

## TIDAL

Strengths:

- High-quality audio positioning.
- Useful for users who value audio fidelity.

Risks:

- TIDAL content and artwork must follow TIDAL attribution and design rules.
- Catalog availability varies.

Agent instructions:

- Use the shared search protocol.
- Preserve platform links where possible.
- Do not alter, crop, overlay, or bundle TIDAL artwork.

## NetEase Cloud Music

Strengths:

- Useful for Chinese-language users.
- Localized metadata and comments can help Chinese beginners.

Risks:

- International classical metadata can be inconsistent.
- Some versions may be unavailable by region or membership tier.
- Platform images and comments should not be republished as open assets.

Agent instructions:

- Search both Western names and Chinese names.
- Use catalog numbers where possible.
- Confirm the recording rather than relying on localized title alone.
- Record Chinese title variants for user convenience.

