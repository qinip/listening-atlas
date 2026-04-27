# Peking Opera Extension Stub

Status: design stub. Use this as a starting point for a real Peking opera project, then revise after an execution run.

## Scope

Peking opera is a performance-art domain. A playable item may be an audio track, video performance, archival transfer, film excerpt, or non-streaming archive page. The core identity is often play, excerpt, school, role type, performer, accompanist, and recording context rather than a single composer.

## Field Additions

Add these fields when useful:

| Field | Rationale |
| --- | --- |
| `creator_role` | Tradition, playwright, school founder, lead performer, arranger, or collective source. |
| `play_title` | Full play. |
| `excerpt_title` | Excerpt or scene. |
| `school` | Mei, Cheng, Xun, Shang, Yu, Yan, Ma, Tan, Yang, etc. |
| `role_type` | Sheng, dan, jing, chou, and subtypes. |
| `vocal_pattern` | Xipi, erhuang, yuanban, manban, kuaiban, liushui, sanban, daoban, etc. |
| `lead_performer` | Main performer. |
| `supporting_performers` | Supporting cast. |
| `accompanist` | Jinghu or other important accompanist. |
| `recording_year` | Recording or performance year. |
| `recording_format` | 78rpm, LP, live, studio, film, broadcast, digital, archival transfer. |
| `playable_type` | `audio_track`, `video`, or `archival_only`. |
| `archive_source` | Archive, collection, upload channel, or institution. |

Core field guidance:

- `composer` may be `traditional`, a school, a lead performer, or `not_applicable`, but the column should stay present.
- `composer_ipa` is usually not useful; use a domain field such as pinyin in the extension rows if needed.
- `work` should identify the excerpt users will search for.

## Match Status Additions

Allowed extension values:

- `different_school`
- `different_accompanist`
- `different_recording_era`
- `different_transfer`
- `live_vs_studio_mismatch`
- `archival_only`

## Platform Notes

Primary platforms may include NetEase Cloud Music, QQ Music, Bilibili, YouTube, and specialist archive sites. Apple Music, Spotify, and TIDAL are usually secondary for this domain.

Execution agents should:

- Treat video as primary when visual performance is essential.
- Prefer official, institutional, or well-described archival uploads.
- Record source channel, archive source, performer, school, recording year, and format.
- Keep unavailable or archival-only rows in the execution log rather than dropping them.

## Chapter Model Sketch

1. Formation: late Qing and early Peking opera.
2. Laosheng schools and early recordings.
3. Four great dan actors and dan schools.
4. Jing and chou roles.
5. Vocal patterns and listening technique.
6. Martial and civil plays.
7. Old records and transfer traditions.
8. Model operas and revolutionary modern works.
9. Reform-era and contemporary Peking opera.
10. Film, overseas circulation, and cross-genre performance.

## Visual Strategy

Use self-drawn school and role-type diagrams, face-pattern diagrams only when the drawing itself is reusable, public-domain playbills, and carefully reviewed public-domain or openly licensed photographs. Many twentieth-century publicity photos and stills remain protected; do not bundle them without item-level rights review.
