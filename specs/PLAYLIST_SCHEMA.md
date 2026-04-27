# Playlist Schema

This schema defines the platform-agnostic source table for generated playlists. Platform-specific fields may be added as case-study extensions, but they should not replace the core fields.

## Core Fields

| Field | Required | Description |
| --- | --- | --- |
| `chapter` | yes | Chapter label and order. |
| `period_range` | yes | Approximate historical range. |
| `genre_or_form` | yes | Form or medium, such as symphony, opera, chant, film score, or game score. |
| `track_no` | yes | Stable playlist order. |
| `after_1900` | yes | Boolean or localized yes/no marker. |
| `composer` | yes | Composer name in the output language or source language. |
| `composer_zh` | optional | Chinese composer name when needed. |
| `composer_western` | optional | Western or source-language composer name when different from `composer`. |
| `composer_ipa` | optional | Pronunciation helper. |
| `composer_wiki` | optional | Reference URL. |
| `work` | yes | Work or excerpt title. |
| `recommended_recording` | yes | Recommended album, release, or canonical recording label. |
| `performers` | yes | Performer, conductor, ensemble, vocalist, or production credits. |
| `search_keywords` | yes | Platform-neutral search query. |
| `difficulty` | yes | Basic, advanced, or custom scale. |
| `role` | yes | Why this row exists in the guide. |

## Optional Fields

| Field | Description |
| --- | --- |
| `fallback_recording` | A second acceptable recording when the preferred one is unavailable. |
| `catalog_number` | BWV, K., Hob., Op., D, RV, Sz., BB, or similar catalog number. |
| `duration_target` | Expected duration range for platform matching. |
| `listening_note` | One-sentence listening instruction. |
| `region_or_tradition` | Cultural region, school, court, city, or national tradition. |
| `medium_pathway` | Concert hall, church, opera, recording, film, game, streaming, etc. |

## Platform Case-Study Fields

The original sample includes `apple_search_keywords`. Keep it when documenting the Apple Music case study, but do not require other platforms to use this field.

For new projects, prefer:

- `search_keywords` for the source table.
- `platform` for the execution target.
- `platform_query` for the exact query used in a specific platform.
- `platform_result_title` for the selected platform result.
- `platform_result_url` when a stable URL exists.
- `platform_match_status` for exact, acceptable, fallback, unavailable, duplicate, or rejected.

## Default Ratios

For a broad beginner-to-intermediate classical music guide:

- 50 tracks: 5 to 7 chapters, fewer advanced works, no obligation to cover every major composer.
- 100 tracks: 8 to 10 chapters, stronger representation across eras and media.
- 180 tracks: 10 chapters, enough room for early music, opera, contemporary music, film, game, and comparison paths.
- Post-1900 default: about 55% to 65% if the goal includes modern listening pathways.
- Difficulty default: about 55% to 65% basic and 35% to 45% advanced.
- Film/game/media chapter default: 5% to 10% when included.

## Acceptance Rules

- Every row must be searchable by composer plus work.
- Every recommended recording must name at least one performer, conductor, ensemble, or release.
- Every chapter must have a clear educational reason.
- The final playlist order must be stable and reproducible.
- Platform execution data must not overwrite source metadata.

