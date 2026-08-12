# Load Log — PWA

A installable, offline-capable hours tracker. Everything lives in the browser via
`localStorage` — no backend, no account, no data leaves the device it's installed on.

## Files
- `index.html` — the app
- `manifest.json` — PWA metadata (name, icons, colors, display mode)
- `service-worker.js` — caches the app shell so it loads and works offline after the first visit
- `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`, `apple-touch-icon.png` — app icons

## Deploy on GitHub Pages
1. Create a new GitHub repo (or a folder in an existing one).
2. Upload all the files in this package to the **same folder**, keeping filenames as-is —
   the manifest and service worker reference them by relative path.
3. In the repo: **Settings → Pages → Deploy from a branch**, pick `main` (or your default
   branch) and the folder (`/root` or `/docs`, whichever you uploaded into).
4. Wait a minute for it to publish, then open the URL GitHub gives you.
5. **Important:** PWAs require HTTPS to install and to register a service worker.
   GitHub Pages serves HTTPS automatically, so this works out of the box.

## Installing it
- **Android / Desktop Chrome / Edge:** an "Install app" button appears in the app header
  once the browser decides it's installable (usually needs the page to be visited over
  HTTPS with the service worker registered). You can also use the browser's own
  "Install app" / "Add to Home Screen" option in the address bar or menu.
- **iOS Safari:** Safari doesn't support the install prompt API. Open the site, tap the
  Share icon, then "Add to Home Screen."

## Notes
- Data is stored per-browser, per-device (`localStorage`). It does **not** sync between
  devices and isn't visible to anyone else — including whoever hosts the repo.
- If you edit `index.html` after deploying, bump `CACHE_VERSION` at the top of
  `service-worker.js` (e.g. `loadlog-v2`) so installed users actually get the update
  instead of a cached copy.
- The Excel export library and fonts load from a CDN. They're cached after first use, so
  export keeps working offline once the app has been opened online at least once.
