# Habitat — installable web app

A self-contained habit companion. No account, no server, works offline once loaded.
This folder is a ready-to-deploy **GitHub Pages** bundle. When someone opens the
published link on their phone and adds it to their home screen, it installs with the
Habitat icon and opens fullscreen like a real app — and installing is what keeps their
saved progress safe from browser storage clearing.

## Files
- `index.html` — the app
- `manifest.webmanifest` — app name, colours, and home-screen icons
- `service-worker.js` — offline caching (see versioning note below)
- `icons/` — home-screen icons (Apple touch icon + 192/512 for Android)
- `.nojekyll` — tells GitHub Pages to serve files as-is

## Deploy in ~3 minutes
1. Create a new GitHub repository (e.g. `habitat`). Public is fine.
2. Upload **everything in this folder** to the repo root — keep the `icons/` folder
   and the `.nojekyll` file. (Drag-and-drop works: GitHub → *Add file* → *Upload files*.)
3. In the repo, go to **Settings → Pages**.
4. Under *Build and deployment*, set **Source: Deploy from a branch**, branch **main**,
   folder **/ (root)**. Save.
5. Wait ~1 minute, then open the URL Pages gives you, e.g.
   `https://YOURNAME.github.io/habitat/`.

It must be the `https://…github.io/…` link (not a file on your computer) — the offline
install features only work over HTTPS.

## Add to home screen (what your customers do)
- **iPhone/iPad (Safari):** open the link → tap **Share** → **Add to Home Screen**.
- **Android (Chrome):** open the link → tap the **⋮** menu → **Add to home screen** /
  **Install app**.

The app also nudges people to do this during onboarding.

## Updating the app later
When you replace `index.html` or any icon, **bump the cache version** so returning
visitors don't keep the old copy:

- Open `service-worker.js`
- Change `const CACHE = 'habitat-v1';` to `'habitat-v2'` (then `v3`, etc.)
- Re-upload. Returning users get the new version on their next visit.

## Notes
- All data stays on the user's device (localStorage). There is no backend and nothing
  is collected.
- Fonts load from Google Fonts on first visit and are then cached for offline use.
