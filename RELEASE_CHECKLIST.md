# Release Checklist

Before publishing this repository:

- Confirm `README.md` and `README.zh-CN.md` are separate language entry points.
- Confirm core docs, specs, prompts, and templates are not interleaved bilingual documents.
- Confirm `products/zh-CN/` and `products/en/` both contain finished guide and playlist files.
- Confirm `site/index.html` and `site/en/index.html` both exist and link to each other in the top-right language switch.
- Confirm release ZIP files exist in `release-assets/`.
- Confirm no `.py`, `.swift`, `.applescript`, shell scripts, binary helpers, credentials, cookies, or browser profiles are present.
- Confirm sample output is clearly labeled as Apple Music case study where platform-specific fields appear.
- Confirm every bundled visual asset appears in an asset manifest.
- Confirm no platform album art, artist image, thumbnail, or screenshot is bundled without separate license review.
- Confirm `LICENSE.md` is present and third-party exceptions are noted.

