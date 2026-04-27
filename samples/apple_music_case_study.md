# Apple Music Case Study

This case study documents lessons from building the sample playlist on Apple Music / Apple Music Classical. It preserves execution knowledge without making Apple Music a required platform.

## Sample Output

- Playlist size: 180 tracks
- Chapters: 10
- Post-1900 tracks: 108
- Pre-1900 tracks: 72
- Basic tracks: 104
- Advanced tracks: 76
- Source guide: `classical_music_intro_guide.zh-CN.md`
- Source table: `classical_music_intro_playlist.apple-music-case-study.tsv`

## What Worked

- Composer plus work plus performer is usually better than work title alone.
- Catalog numbers reduce ambiguity for Bach, Mozart, Haydn, Schubert, Vivaldi, Debussy, Ravel, Bartok, and similar composers.
- Apple Music Classical is more useful than general Apple Music for work-level search.
- Multi-movement works require movement-level verification.
- A TSV table with stable `track_no` makes retries and audit logs much easier.

## Common Failure Modes

- Search picks the wrong movement from the right work.
- Search picks the right work but a different performer.
- Search picks a transcription, arrangement, excerpt, or live clip when the guide expects a specific recording.
- Add-to-playlist actions appear successful but do not change playlist count.
- Regional catalog differences make a recommended recording unavailable.

## Practical Rule

If a result cannot be justified by title, composer, movement, performer, and release context, mark it as `fallback` or `rejected` instead of silently accepting it.

## What Not To Release

Do not include local Apple Music automation scripts, accessibility helpers, account-specific logs, browser state, screenshots, platform images, or binary helpers in the open kit.

