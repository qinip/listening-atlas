# Jazz Extension Stub

Status: design stub. Use this as a starting point for a real jazz project, then revise after an execution run.

## Scope

Jazz often treats a recording as the primary musical object. The same standard can become different works when the leader, personnel, session date, take, venue, or label context changes.

## Field Additions

Add these fields when useful:

| Field | Rationale |
| --- | --- |
| `recording_id` | Stable identity for the recording-level object. |
| `standard_composer` | Composer of the tune or standard; distinct from the recording leader. |
| `recording_leader` | Leader of this recording or session. |
| `ensemble_name` | Fixed group name, if any. |
| `personnel` | Structured `Name (instrument); Name (instrument)` lineup. |
| `session_date` | Session or performance date. |
| `session_location` | Studio, club, festival, city, or venue. |
| `label_catalog` | Label and catalog identifier when known. |
| `take` | Master take, alternate take, live version, or edition marker. |
| `is_alternate_take` | Flags alternate-take identity risk. |
| `live_or_studio` | Live, studio, broadcast, rehearsal, or unknown. |
| `scene` | Kansas City swing, bebop, hard bop, modal, AACM, ECM, fusion, etc. |
| `label_arc` | Blue Note, Impulse, ECM, Savoy/Dial, Bandcamp independent era, etc. |
| `matrix_number` | Useful for early jazz and 78rpm transfers. |
| `discography_reference` | Jazzdisco, Tom Lord reference, or other session-level source when available. |

Core field guidance:

- `composer` may be the recording leader for browsing stability.
- `work` should be the track title as released.
- `recommended_recording` should name the album/release and, where possible, catalog context.
- `playable_type` is usually `audio_track`, but may be `video` for historically important footage.

## Match Status Additions

Allowed extension values:

- `wrong_take`
- `wrong_master`
- `compilation_substitute`
- `remaster_difference`
- `wrong_personnel`
- `wrong_session`

## Platform Notes

Primary platforms usually include Apple Music, Spotify, TIDAL, Qobuz, YouTube Music, and Bandcamp for contemporary independent releases.

Execution agents should:

- Search by `recording_leader + work + album/release` before using composer names.
- Verify personnel, session date, catalog, live/studio status, and take when visible.
- Record compilation and remaster substitutions explicitly.
- Treat anniversary, deluxe, mono, stereo, and live editions as version-sensitive.

## Chapter Model Sketch

1. Origins: New Orleans, blues, ragtime, early recording.
2. Swing and big band.
3. Bebop.
4. Cool, West Coast, and Third Stream.
5. Hard bop and Blue Note.
6. Modal and the long 1960s.
7. Free jazz and AACM.
8. Fusion and electric jazz.
9. ECM and European scenes.
10. Contemporary jazz after 2000.
11. Cross-cutting listening chapter: head-solos-head, piano trio, modal vs. changes, free vs. structured.

## Visual Strategy

Use public-domain early photographs, Library of Congress images, self-drawn lineup diagrams, scene networks, and label-era diagrams. Do not bundle Blue Note covers, Francis Wolff photographs, or copyrighted promotional photos unless a separate reusable license is documented.
