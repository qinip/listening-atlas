# Samples

This folder contains case-study material from the original Apple Music playlist project.

## Files

- `classical_music_intro_guide.zh-CN.md`: original Chinese sample guide.
- `classical_music_intro_playlist.apple-music-case-study.tsv`: 180-track playlist dataset with Apple Music search keywords as a case-study field.
- `apple_music_case_study.md`: lessons learned from executing the sample on Apple Music / Apple Music Classical.
- `ebook_sample.html`: early static HTML layout sample with no JavaScript and no bundled third-party images.

## Boundary

The Apple Music sample is a reference implementation, not a dependency. New users should adapt the platform adapter to their own platform and keep the source dataset platform-agnostic.

The finished `products/` packages are cleaned Classical Atlas demo releases derived from this Apple Music path. They are still Apple Music case-study editions; the reusable platform-agnostic kit contract lives in `specs/`, `prompts/`, and `templates/`.
