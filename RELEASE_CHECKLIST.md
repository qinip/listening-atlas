# Release Checklist

Before publishing this repository:

- Confirm `README.md` and `README.zh-CN.md` are separate language entry points.
- Confirm core docs, specs, prompts, and templates are not interleaved bilingual documents.
- Confirm `products/zh-CN/` and `products/en/` both contain finished guide and playlist files.
- Confirm `site/index.html` and `site/en/index.html` both exist and link to each other in the top-right language switch.
- Confirm release ZIP files exist in `site/downloads/` for GitHub Pages links and in local `release-assets/` only as ignored upload staging.
- Confirm no `.py`, `.swift`, `.applescript`, shell scripts, binary helpers, credentials, cookies, or browser profiles are present.
- Confirm `specs/DELIVERABLES.md` names the required outputs clearly.
- Confirm `specs/PLATFORM_EXECUTION_LOG_SCHEMA.md` can log one row per source playlist row.
- Confirm optional visual and appendix work follows `specs/VISUAL_AND_APPENDIX_MODULES.md`.
- Confirm sample output and product packages are clearly labeled as Apple Music case-study editions where platform-specific fields appear.
- Confirm every bundled visual asset appears in an asset manifest.
- Confirm no platform album art, artist image, thumbnail, or screenshot is bundled without separate license review.
- Confirm `LICENSE.md` is present, split CC0 / CC BY licensing is clear, and third-party exceptions are noted.
