# Prompt 06: QA Review

Use this prompt before publishing.

```text
Review this Listening Atlas output against the quality checklists and deliverables contract.

Check:

- Reproducibility: Can a new agent follow the instructions without private context?
- Deliverables: Are the required files in `specs/DELIVERABLES.md` present and named clearly?
- Platform independence: Does the source dataset work outside the original platform?
- Platform execution: Is there a complete execution log with one row per source row and order verification?
- Content balance: Are eras, regions, genres, modern music, and difficulty levels aligned with the brief?
- Guide linkage: Do chapter entry works and appendices point back to `track_no` or stable row identifiers?
- Version safety: Are recordings identifiable and are ambiguous matches flagged?
- Asset safety: Are all bundled visuals in the asset manifest with source, creator, license, and attribution?
- Pages readiness: Are the Chinese and English static ebook pages linked with a visible language switch?
- Release safety: Are there any automation scripts, binaries, secrets, cookies, platform screenshots, or unlicensed assets?

Return blocking issues, non-blocking improvements, suggested release notes, and a final publish/no-publish recommendation.
```
