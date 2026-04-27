# Platform Execution Log Schema

The platform execution log records the real work done inside Apple Music, Spotify, YouTube Music, YouTube, TIDAL, NetEase Cloud Music, or another service. It is separate from the source playlist TSV.

Use `templates/platform_execution_log.template.tsv`.

## Required Fields

| Field | Required | Description |
| --- | --- | --- |
| `track_no` | yes | Source playlist order. Must match the source TSV. |
| `source_work` | yes | Work or excerpt from the source TSV. |
| `source_composer` | yes | Composer or creator from the source TSV. |
| `platform` | yes | Target platform. |
| `playlist_name` | yes | Playlist being created or edited. |
| `query_attempt` | yes | `strict`, `medium`, `fallback`, `manual`, or `not_searched`. |
| `platform_query` | yes if searched | Exact query typed or pasted. |
| `selected_title` | yes if added | Visible selected track or video title. |
| `selected_creator_or_artist` | recommended | Visible artist, performer, channel, or album artist. |
| `selected_album_or_source` | recommended | Album, release, video, channel, or collection where visible. |
| `selected_duration` | recommended | Duration shown by the platform, if visible. |
| `selected_url` | recommended | Stable platform URL if the platform exposes one. |
| `match_status` | yes | `exact`, `acceptable`, `fallback`, `unavailable`, `duplicate`, `rejected`, or `needs_human_review`. |
| `fallback_used` | yes | `yes` or `no`. |
| `expected_order` | yes | Expected playlist position from source order. |
| `final_order` | yes if order can be inspected | Actual playlist position after creation. |
| `order_status` | yes | `verified`, `moved`, `not_visible`, `not_applicable`, or `needs_human_review`. |
| `notes` | recommended | Short reason for substitutions, rejects, or uncertainty. |

## Match Status Rules

- `exact`: composer/work/movement and key performer or release match the source row.
- `acceptable`: work and movement are correct, but performer or release differs in a way allowed by the brief.
- `fallback`: preferred recording unavailable; a documented fallback was used.
- `unavailable`: no acceptable result was found.
- `duplicate`: row appears already added or platform created a duplicate.
- `rejected`: visible result was wrong or too uncertain.
- `needs_human_review`: the agent cannot confidently decide.

## Order Verification

After adding tracks, the execution agent must inspect the platform playlist order if the platform UI allows it.

Required checks:

- `track_no` 001 should appear before 002, 002 before 003, and so on.
- Missing rows must remain visible in the log as `unavailable`, `rejected`, or `needs_human_review`.
- If the platform added a result to the wrong position, move it when possible and record `order_status=moved`.
- If the platform UI does not expose the full order, record `order_status=not_visible` and explain the limitation.

## Safety Boundary

Creating or editing a playlist changes a user's cloud account. A platform-execution agent should get clear user approval for the platform, account, playlist name, privacy setting, and whether it may create or edit the playlist before taking action.
