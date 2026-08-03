# ITL Ops

Single-page inventory app. Served from GitHub Pages so it has a real HTTPS
origin — which is what makes sync, installation and offline caching possible.

## Deploying a change

    python3 build.py        # stamps index.html, regenerates version.js/json
    git add -A && git commit -m "..." && git push

The build id is a content hash of `index.html` with the stamp blanked, so it
changes when the app changes and stays put when it doesn't. Rebuilding without
editing gives the same hash.

Open tabs check `version.json` on load, on returning to the app, and hourly.
When the deployed build differs from the running one, a bar offers a reload —
and it pushes any unsaved work before reloading.

## Files

| file | |
|---|---|
| `index.html` | the app; carries `const BUILD` |
| `version.js` | `window.ITL_BUILD`, for anything that wants it as a script |
| `version.json` | what the update check fetches |
| `manifest.json`, `sw.js`, `icon-*.png` | installability and offline |
| `build.py` | run after every edit |

## Do not commit

The shared key. It is entered in the app and lives in your URL fragment, never
in the repo. A public Pages repo means anyone can read this code — that is
fine, since the data sits behind the key on the Worker — but a committed key
would hand over the data with it.
