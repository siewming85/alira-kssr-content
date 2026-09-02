# alira-kssr-content

Over-the-air (OTA) content for the **ALIRA KSSR English Picture Dictionary**
Android app (`mobile/` in the main project).

The app checks this repo on launch (when online) and downloads only the
picture-dictionary files that changed since its bundled baseline — each verified
by SHA-256 — without needing a Play Store release.

## Layout

```
content/manifest.json        # SHA-256 + size index; contentVersion; minAppBuildNumber
content/data/database.json    # merged learning-content export
content/images/*.webp         # every dictionary / comic / poster / scene image
```

Served to the app as:

- manifest: `https://raw.githubusercontent.com/siewming85/alira-kssr-content/main/content/manifest.json`
- files:    `https://cdn.jsdelivr.net/gh/siewming85/alira-kssr-content@main/content/...`

## Publishing

Do not edit this repo by hand. From the main project's `mobile/` directory:

```bash
python tool/prepare_assets.py
python tool/publish_content.py --content-repo <path-to-this-clone>
```

That regenerates the assets + manifest, copies them here, commits, pushes, and
purges the jsDelivr edge cache. See `mobile/tool/README_content_ota.md`.
