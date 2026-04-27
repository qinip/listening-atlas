# Visual And Appendix Modules

These modules are optional. Use them when the project brief asks for a richer ebook, but keep the source playlist TSV and guide Markdown usable without them.

## Music History Map

Purpose: provide a visual overview of eras, regions, genres, composers, and representative works. The map does not need to include every playlist row.

Recommended data fields:

| Field | Description |
| --- | --- |
| `node_id` | Stable identifier. |
| `node_type` | `era`, `composer`, `work`, `genre`, `medium`, or `tradition`. |
| `label` | Display label. |
| `display_year` | Approximate timeline anchor. |
| `period_range` | Broad range when a single year is misleading. |
| `region_or_tradition` | Region, school, cultural sphere, or platform-medium category. |
| `color_group` | Visual grouping, usually region/tradition/medium. |
| `source_track_no` | Optional playlist row that the node represents. |
| `image_asset_id` | Optional portrait or artwork from the asset manifest. |
| `notes` | Why the node appears. |

Output options:

- Static SVG embedded in HTML.
- Static HTML/CSS layout.
- PNG generated from a reviewed local source.

Do not rely on JavaScript for the first release. If portraits are used, each image must be in the asset manifest.

## Chapter Images

Chapter images should help the reader understand the chapter's setting or medium. They should not be a repetitive gallery of composer headshots.

Good chapter image types:

- Public-domain paintings of musical performance, courts, opera houses, salons, or instruments.
- Manuscript pages or notational examples with reusable rights.
- Public-domain stage or production stills when rights are clear.
- Self-generated illustrations when the asset policy allows them.
- Carefully licensed portraits only when the chapter centers on a person.

Bad chapter image types:

- Platform album art copied from a streaming service.
- Generic stock-looking musical instruments.
- Cropped portraits that cut off faces or remove context.
- Images with unclear source, creator, license, or reuse permission.

## Appendices Linked To Playlist Rows

Appendices should not float away from the source playlist. When useful, include row references:

- Composer index: include names, pronunciation aids, region/tradition, and representative `track_no` values.
- Catalog-number appendix: explain BWV, K., Hob., Op., D., RV, Sz., BB, and link examples to rows.
- Recording comparison appendix: explain how to compare versions and reference a few rows where versions matter.
- Glossary: define terms and link to chapters or rows where the term can be heard.
- Platform appendix: explain platform-specific search or playback links only as execution notes, not source truth.

## Platform Links In The Guide

If the platform execution log includes stable links, the HTML ebook may link entry works to platform playback or search pages.

Rules:

- Keep source playlist metadata platform-agnostic.
- Label platform links as platform links, not canonical sources.
- If a link points to a user's private playlist or account-specific surface, do not publish it.
- If a row was substituted, the guide should not silently present it as the original preferred version.
