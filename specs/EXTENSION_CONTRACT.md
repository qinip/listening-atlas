# Extension Contract

Listening Atlas has a small core schema, but some domains need additional structure. Do not add a new workflow phase for every genre. Use a domain extension when the core fields are not enough.

## When To Use An Extension

Use an extension if the project has one or more of these differences:

- Identity model: the musical object is not simply `composer + work`.
- Personnel granularity: named performers, lineups, accompanists, or ensembles define the object.
- Version sensitivity: take, master, school, recording date, remaster, live/studio status, or transfer source changes the identity.
- Playable medium: video, performance footage, archival pages, or non-streaming sources are primary.
- Platform fit: the best platforms are not the default Western streaming platforms.
- Asset availability: expected visuals are mostly unavailable for open reuse.
- Repertoire model: chronology alone is not the right chapter axis.

## Core Invariants

Extensions may not redefine these rules:

- `row_id` is stable and unique.
- `track_no` is stable, sortable, and owns final order.
- The source playlist TSV remains the source of truth for editorial identity and sequence.
- The platform execution log remains the source of truth for platform-specific search, selected result, fallback, unavailable rows, and final order.
- Platform artwork, account data, comments, cookies, screenshots, and private URLs must not become source truth.
- Every extension-specific field must have a rationale tied to one of the differential axes above.

## Allowed Extension Behavior

An extension may:

- Add fields to the source TSV.
- Add fields to the execution log.
- Mark a core field as `not_applicable` for a domain, while keeping the column present for interoperability.
- Add domain-specific `match_status` values.
- Define a chapter model, platform priority order, visual strategy, and appendix strategy.
- Define domain-specific search rules.

An extension may not:

- Delete core fields.
- Make platform-specific fields replace platform-neutral source fields.
- Require API access or automation scripts.
- Bundle unreviewed images, album art, screenshots, or platform thumbnails.

## Extension File Shape

Each extension should include:

1. Domain scope and assumptions.
2. Field additions and semantic overrides.
3. Platform priority and search rules.
4. Match-status additions.
5. Recommended chapter model.
6. Visual and asset policy notes.
7. Known hard limits.

Use `specs/extensions/jazz.md` and `specs/extensions/peking_opera.md` as stub examples. They are intentionally partial until real projects validate them.
