# Composer's Bench — installable app (PWA)

This is your app packaged as a **Progressive Web App**: it can be installed to a phone's
home screen, opens full-screen like a native app, and works offline.

## Files (put ALL of them in your repo, same folder)

- `index.html` — the app (with manifest + service worker hooks)
- `manifest.webmanifest` — app name, colours, icons
- `sw.js` — service worker (offline caching)
- `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` — app icons
- `apple-touch-icon.png` — iOS home-screen icon

Keep them all in the **same directory** and use the filenames as-is.

## Deploy to GitHub Pages

1. Commit all the files above to your repo (root, or a folder — just keep them together).
2. **Settings → Pages → Deploy from a branch → `main` / `/root` → Save.**
3. Open `https://<you>.github.io/<repo>/` on your phone.

A service worker only runs over **https** (GitHub Pages is https), so installation and
offline work once it's hosted — not from a local `file://` open.

## Install it

- **Android (Chrome/Samsung Internet):** open the site, then menu → **Add to Home screen**
  / **Install app**. You may also get an automatic install prompt.
- **iPhone (Safari):** open the site, tap **Share → Add to Home Screen**.

It launches full-screen with the piano icon, no browser chrome.

## Offline behaviour

- The **app itself works offline** immediately after the first visit — the service worker
  caches the app shell. All music features (keyboard, chords, timeline, drums, synth
  voices, MIDI/MusicXML import & export) run with no network.
- The **real piano samples** are cached the first time they load while online; after that
  the sampled Grand piano works offline too. (Until then, offline sessions use the
  synthesized piano, which needs no download.)

### Want the samples available before the first online load?

Download a piano sample set (e.g. Salamander Grand, or `tonejs-instruments`) into a
`samples/` folder in the repo, then in the app's **About → Real piano samples** field
enter `samples/` and press Load. The service worker will cache those too.

## Updating the app

When you replace `index.html` with a new build, bump the cache name in `sw.js`
(`composers-bench-v1` → `-v2`) and commit both. The service worker will fetch the new
version and drop the old cache on next load.

## About the AI features

The mentor chat, Critique, Rewrite, and Suggest-a-bassline need a server to hold an API
key, so they don't run on a plain static/PWA deploy — everything else does. Ask if you
want the small backend proxy that enables them.
