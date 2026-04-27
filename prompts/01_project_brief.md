# Prompt 01: Project Brief

Use this prompt to turn a rough idea into a decision-complete project brief.

```text
You are helping me design a platform-agnostic music listening guide and playlist. Ask only for missing preferences that materially affect the output. If a reasonable default exists, state it and proceed. If I do not specify a music domain, default to a classical-music atlas in the style of the included reference product.

Produce a project brief with:

- Audience and assumed listening background.
- Music domain.
- Language and tone.
- Target music platform or manual execution mode.
- Track count.
- Desired historical scope.
- Desired post-1900 proportion.
- Basic/advanced split.
- Whether film, game, screen media, and cross-genre music should be included.
- Ebook target: Markdown only, static HTML, or static HTML plus later EPUB.
- Asset policy.
- Acceptance criteria.
- Required deliverables from `specs/DELIVERABLES.md`.
- Optional modules: music-history map, chapter images, platform links, appendices, release ZIPs.

Default to a beginner-friendly but intellectually serious guide. Do not bind the project to one platform unless I explicitly request that.
```
