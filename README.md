# Composer's Bench

A browser-based piano composition studio: playable keyboard, diatonic + color chords,
progression builder, melody + bassline, timeline with drag-positioning, drums, multiple
instrument voices, and MIDI export.

This is a **static site** — just HTML + JavaScript. No build step, no server needed.

## Files

- `index.html` — the page
- `app.js` — the whole app bundled into one file (React, Tone.js, and the app)

## Deploy to GitHub Pages

1. Create a new repository on GitHub (e.g. `composers-bench`).
2. Add `index.html` and `app.js` to the repo (drag them into the web uploader, or commit and push).
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**, pick your
   branch (usually `main`) and the `/root` folder, then **Save**.
5. Wait ~1 minute. Your app is live at `https://<your-username>.github.io/<repo-name>/`.

That's it. Open the page, click a key, and the **Grand piano** voice will load real
recorded samples automatically (see below).

### Test locally first (optional)

Because the app fetches audio samples, open it through a local server rather than
double-clicking the file:

```bash
# from this folder
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Real piano samples

The **Grand piano** voice loads the free **Salamander Grand** samples from
`https://tonejs.github.io/audio/salamander/`. Once the app is hosted (or run from a
local server), the browser can fetch them and the sound upgrades from the synthesized
piano to the real recorded one. The status line under the title shows
"♪ Grand piano (sampled)" when it's active.

### Use your own samples (optional, for offline / full control)

1. Download a sample set (e.g. the Salamander Grand, or the `samples/piano` folder from
   the `tonejs-instruments` project). You need files named by pitch, e.g.
   `A4.mp3`, `C4.mp3`, `Ds4.mp3`, `Fs4.mp3` …
2. Put them in a `samples/` folder next to `index.html` and commit them.
3. In the app, open the **About** tab, and under **Real piano samples** paste your
   folder's URL (for a same-repo folder that's just `samples/`) and press **Load**.

Bundling samples this way makes the app work offline and independent of any outside site.

## About the AI features

Four features use Anthropic's API: the mentor chat, progression **Critique** and
**✦ Rewrite**, and **Suggest a bassline**. These need a server to hold your API key —
a static site can't (a key in client-side code would be public and would be blocked by
the browser anyway). On a plain GitHub Pages deploy these buttons will simply show a
"couldn't reach the mentor" message; **everything else works fully client-side.**

To enable them you'd add a small backend proxy (e.g. a serverless function) that holds
your key and forwards requests to `https://api.anthropic.com/v1/messages`, then point the
app's fetch at that proxy. Happy to help wire that up if you want it.

## What works with no server

Keyboard, scales, diatonic + color chords, progression builder, per-chord octave/length/feel,
melody, timeline drag-positioning + rests, tempo (incl. separate chord/melody tempo),
drums, instrument voices, real piano samples, and **MIDI export** — all run entirely in
the browser.
