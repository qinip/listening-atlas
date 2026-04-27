# Demo Release Notes

Use this text for the GitHub Release that attaches the Classical Atlas ZIP files.

## What This Release Contains

This release contains the **Classical Atlas demo products**:

- `classical-atlas-zh-CN.zip`: Chinese Apple Music edition demo package.
- `classical-atlas-en.zip`: English Apple Music edition demo package.

Each ZIP includes the finished guide, static HTML ebook, playlist TSV, reconstructed Apple Music execution log, package prompt, license file, third-party notices, and bundled visual assets with an asset manifest.

## What The Main Deliverable Is

The main open-source deliverable is **not** the demo ZIP alone. The reusable Listening Atlas Agent Kit is the repository itself:

- `docs/`
- `specs/`
- `prompts/`
- `templates/`

Use the repository kit to generate your own music-domain guide, platform-agnostic playlist TSV, platform execution log, and optional HTML ebook.

## Demo Boundary

The Classical Atlas packages are Apple Music case-study editions. Apple Music search columns and package prompts are intentional demo details, not requirements for other platforms. For Spotify, YouTube Music, YouTube, TIDAL, Qobuz, Bandcamp, NetEase Cloud Music, QQ Music, Bilibili, or other services, use `prompts/04_platform_execution.md` and `specs/PLATFORM_ADAPTERS.md`.

## Licensing

The reusable kit materials are CC0 1.0. Demo guide text, playlist data, reconstructed execution logs, and HTML layout are CC BY 4.0. Third-party visual assets retain the licenses recorded in each package's `assets/ASSET_MANIFEST.tsv`.
