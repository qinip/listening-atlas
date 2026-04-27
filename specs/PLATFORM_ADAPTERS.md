# Platform Adapters

This file describes how a computer-use agent should execute the same playlist spec on different music platforms. It is a protocol, not code.

## Shared Execution Protocol

For every platform:

1. Read one playlist row.
2. Search with `strict_search_query` when present, otherwise `composer + work + key performer`.
3. If the result is noisy, use `medium_search_query` and then `fallback_search_query`.
4. Confirm title, composer, movement, performer, conductor, ensemble, album/release, and duration when visible.
5. Add only one best match.
6. Record match status: exact, acceptable, fallback, unavailable, duplicate, or rejected.
7. Record the result in the platform execution log schema.
8. Verify final playlist order against `track_no`.
9. Keep platform URLs or screenshots as local execution notes, not as source truth.
10. Do not download or package platform artwork.

If the source row has `playable_type=video`, `audio_and_video`, or `archival_only`, do not force it into a normal audio-track match. Record the selected playable type in the execution log. If the row can only be represented by an archive page, keep it in the log with a documented `external_archive_url` and an extension-defined match status such as `archival_only`.

## Playable Type Modes

### Audio Track

The normal case for most Western streaming services. Use the shared search protocol and add one best audio result.

### Audio And Video

Use when either a streaming track or a performance video can satisfy the row. Record which one was selected and why.

### Video Primary

Use for opera scenes, Peking opera, dance, theater music, live performance traditions, game performance footage, or other domains where visual performance is part of the musical object.

Agent instructions:

- Prefer official, institutional, artist, label, opera house, theater, festival, or archive channels.
- Record source channel, visible title, duration, and whether the video is official, archival, live, broadcast, or user-uploaded.
- Do not treat the video thumbnail or still frame as reusable artwork.

### Archival Only

Use when the row is historically important but unavailable as a normal platform item.

Agent instructions:

- Keep the row in the execution log.
- Record archive source, external URL, and reason it is accepted.
- Do not count the row as a normal streaming playlist item unless the project brief allows mixed playlist/archive outputs.

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

## Qobuz

Strengths:

- Strong catalog for classical, jazz, high-resolution releases, and album-level metadata.
- Useful when label, catalog, and audio quality matter.

Risks:

- Availability varies by country.
- Playlist and sharing behavior may be less familiar to some agents.
- Artwork and editorial metadata should not be republished as open assets.

Agent instructions:

- Search by artist/leader, work or track title, album, label, and catalog context.
- Record release and quality context when visible.
- Preserve links in the execution log when stable.

## Bandcamp

Strengths:

- Important for contemporary jazz, experimental, independent, electronic, and local scenes.
- Often has releases that are missing from mainstream streaming platforms.

Risks:

- It is release-first, not always playlist-first.
- User accounts, purchases, downloads, and messages are out of scope unless the user explicitly asks.
- Album art and artist images are not reusable unless separately licensed.

Agent instructions:

- Treat Bandcamp as release discovery and listening support unless the brief explicitly defines a Bandcamp collection workflow.
- Do not purchase, download, or follow without user confirmation.
- Record release URL, artist, label, and track URL where available.

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

## QQ Music

Strengths:

- Useful for Chinese-language music, local catalog coverage, and some opera or traditional-performance recordings.

Risks:

- Metadata and rights availability vary by region and account tier.
- Platform imagery, comments, and social data must not be republished.

Agent instructions:

- Search with Chinese title, performer, excerpt, and source-language variants.
- Record localized title variants and availability limits.

## Bilibili

Strengths:

- Often useful for performance video, archival recordings, opera, theater, game concerts, and educational material.

Risks:

- Upload provenance and rights vary widely.
- Video comments, thumbnails, danmaku, and screenshots are not reusable release assets.
- Video links may disappear.

Agent instructions:

- Prefer official, institutional, verified, archive, theater, broadcaster, or performer channels.
- Record uploader/channel, video title, duration, and reason for acceptance.
- Use as primary only when the brief or domain extension allows video-primary execution.

## Order And Completion Rules

- The execution log should have one row for every source playlist row, even if the track is unavailable.
- Do not silently skip unavailable rows.
- After adding tracks, inspect the playlist and verify the visible order whenever the platform allows it.
- If the platform adds tracks at the top rather than the bottom, reorder the playlist or record the limitation.
- If the user wants a public playlist, confirm that privacy setting before creating or publishing it.
