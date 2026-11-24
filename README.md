# SignSpeak AI — Responsive Web + PWA

This package upgrades the supplied SignSpeak AI HTML project for desktop and mobile browsers and adds installable Progressive Web App (PWA) support.

## What is included

- The original SignSpeak AI interface and gesture-recognition/training logic are retained.
- Responsive layouts and mobile touch-target improvements for phones and tablets.
- Phone camera preference selector (rear/front/automatic), while retaining manual camera selection and switching.
- PWA manifest, app icons, install button, service worker and offline fallback page.
- GitHub Pages-compatible relative paths; no backend or paid hosting is required for the static site.
- The service worker caches only same-origin app-shell/static files. It does not cache camera frames, gesture records, history or other personal data.

## Run locally

Camera access needs a secure context. Use localhost rather than opening the HTML file directly:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000` in a modern browser. MediaPipe is loaded from jsDelivr, so an internet connection is needed for the hand-detection library unless the browser already has the required resource available.

## Publish with GitHub Pages

1. Extract this ZIP.
2. Copy the **contents** of `SignSpeak-AI-PWA` into the root of your GitHub repository (the `index.html` file must be at the repository root).
3. Commit and push the files to GitHub.
4. In the repository, open **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**, select your branch (usually `main`) and folder **/(root)**, then save.
6. Open the Pages URL after GitHub finishes deploying. Use the HTTPS URL for camera access and PWA installation.

For a repository named `your-project`, GitHub Pages normally serves it under `https://YOUR-USER.github.io/your-project/`. This package uses relative URLs to support that subpath.

## Install on a phone

- **Android:** open the HTTPS GitHub Pages URL in Chrome, then use the app's **Install App** action or Chrome menu → Install app / Add to Home screen.
- **iPhone/iPad:** open the HTTPS URL in Safari → Share → Add to Home Screen. iOS does not use the same automatic install prompt as Chromium browsers.
- Grant camera permission when starting Live Recognition. Choose Rear camera preferred or Front camera preferred as needed. Browser and device support can vary.

## Important data and privacy notes

The existing app stores trained gestures, settings and history in the browser's local storage on each device. This data is **not automatically synced** between a laptop and a phone, and it is not included in the website files. Before switching to the hosted version, open the current app and use **Gesture Library → Export** or **Settings → Export all data** to download a backup. On the hosted app, unlock the training module, use **Gesture Library → Import**, and select the backup file. Keep the backup somewhere safe.

Browser storage is scoped to the website origin. Data saved on `localhost` will not automatically appear on the GitHub Pages domain. Export/import is the migration path in this static version. Multi-device cloud synchronization would require a separately configured backend and authentication; it is not included here.

The training password check is implemented in client-side browser code. It helps control the training interface in this prototype, but it is not equivalent to server-side authentication and should not be used to protect sensitive data.

## Offline behaviour

The service worker caches the static app shell and offers an offline page if navigation fails. The MediaPipe library is loaded from a third-party CDN and is deliberately not cached by this service worker. Therefore the interface may open offline, but live AI hand detection may require an internet connection.

## Project files

- `index.html` — main application.
- `manifest.webmanifest` — PWA metadata.
- `sw.js` — static-shell service worker.
- `offline.html` — offline fallback.
- `assets/` — application icons.
