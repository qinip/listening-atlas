# Quality Checklists

Use these checklists before publishing a generated playlist, guide, ebook, GitHub Pages site, or release ZIP.

## Reproducibility

- A new agent can follow the repository without private context.
- The agent can fill a project brief.
- The agent can generate 50-track, 100-track, and 180-track playlist drafts.
- The agent can produce the required files listed in `specs/DELIVERABLES.md`.
- The outputs preserve the requested language and audience level.
- The outputs use the platform-agnostic schema, not platform-only fields.

## Platform Execution

- The same playlist spec can be executed on at least two platforms.
- Platform-specific fields are stored as execution notes or case-study fields.
- A platform execution log exists when a streaming playlist was created or edited.
- The execution log has one row per source playlist row.
- Final playlist order is verified against `track_no`, or the platform limitation is explicitly logged.
- Missing tracks are recorded with fallback decisions.
- Duplicates are identified before final ordering.
- No platform artwork, thumbnails, screenshots, or account-specific data are bundled.

## Content

- The playlist has a readable historical sequence.
- The guide Markdown ties entry works back to playlist rows using `track_no` or stable row identifiers.
- Each chapter has enough representative works for its scope.
- Post-1900 proportion matches the project brief.
- Basic/advanced split matches the project brief.
- Film, game, and screen media are included only if requested.
- Regions, traditions, gender representation, and living composers are reviewed for avoidable blind spots.
- Composer names, work titles, catalog numbers, and performer names are internally consistent.

## Assets

- Every bundled image appears in an asset manifest.
- Music-history maps and chapter images follow `specs/VISUAL_AND_APPENDIX_MODULES.md`.
- Each asset has source URL, creator, license, attribution text, and reuse notes.
- Wikimedia Commons assets are checked at file level.
- The Met Open Access assets are marked as CC0 or public domain according to the source page.
- Platform album art and artist images are not bundled unless separately licensed.
- No fair-use-only asset is included in the open release.

## GitHub Pages

- The Chinese and English ebook pages are both reachable.
- Each page has a visible top-right language switch.
- The HTML works without JavaScript.
- Links to release ZIP files are relative and stable.
- The page does not hotlink unreviewed third-party images.

## Release ZIPs

- ZIP files contain finished products only: guide, playlist, ebook, license, and a short readme.
- ZIP files do not contain source prompts unless intentionally included.
- ZIP files do not contain automation scripts, binaries, credentials, cookies, or browser profiles.
- Chinese and English products are packaged separately.

## Repository Release Safety

- No `.py`, `.swift`, `.applescript`, shell script, binary helper, or platform automation code is included in the open kit.
- Sample outputs are labeled as sample output or case study.
- `LICENSE.md` is present.
- Third-party content exceptions are documented.
- Links to platform terms and asset reuse guidance are present where relevant.
