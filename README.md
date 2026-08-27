# Rise Youth Pass

A lightweight installable web app for Rise Youth Middle School check-in passes.

## Complete repo structure

Put these files in the **root** of the GitHub repository:

```text
index.html
manifest.json
sw.js
icon.svg
.nojekyll
README.md
```

The first three files are the v3 files already provided. This support bundle supplies the remaining files.

## What each file does

- `index.html` — the app UI, student pass storage, switching, and QR generation.
- `manifest.json` — tells phones how the installed web app should behave.
- `sw.js` — handles offline/cache behavior and update replacement.
- `icon.svg` — Rise Youth Home Screen/app icon used by `index.html` and cached by `sw.js`.
- `.nojekyll` — tells GitHub Pages to serve the repository as-is instead of applying Jekyll processing.
- `README.md` — project notes only; it does not affect the live app.

## GitHub Pages setup

1. Create a new public GitHub repository.
2. Upload all six files to the root of the repository.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select the `main` branch and `/ (root)` folder.
6. Save.
7. Once Pages is published, open the GitHub Pages URL in Safari on iPhone or Chrome on Android.
8. Add the site to the Home Screen **before** creating the first student pass.

## Important update rule

When changing app behavior later, update the version in both `index.html` and `sw.js`.

For example:

```text
index.html: APP_VERSION = '3.1.0'
sw.js:      CACHE_NAME = 'rise-youth-pass-v3.1.0'
```

Keeping those versions in sync makes it much less likely that an installed copy will continue showing an old build.

## Student data

Student passes are stored in the browser's `localStorage` on that specific device. The app itself does not upload the entered names to a server.

Deleting the Home Screen app/browser site data may remove saved passes, so they would need to be recreated on that device.

## QR library

The current `index.html` loads QRCode.js from cdnjs. This means first-time QR rendering requires network access to that CDN. If a fully self-contained/offline build is desired later, download and host that JavaScript file inside the repo and add it to the service worker cache.
