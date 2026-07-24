# ora-retreats.com

Static marketing site for ora retreats. No build step required.

## Pages

- `index.html` — home (hero, retreat, about, contact sections)
- `retreats.html` — retreats detail, including "see the house" photo mosaic
- `about.html` — about ora / Julie & Rilke
- `contact.html` — contact

## Local preview

Open `index.html` directly in a browser, or serve the folder with any static
file server (e.g. `python -m http.server` from this directory).

## Deploying to easyhost.be

1. Log in to the easyhost.be control panel.
2. Open the file manager (or connect via FTP) for the `ora-retreats.com` hosting product.
3. Upload the entire contents of this folder (`index.html`, `retreats.html`,
   `about.html`, `contact.html`, `css/`, `js/`, `images/`) to the web root.
   Do not upload the `Tommy/` folder — it holds the original, unoptimized
   source assets and isn't tracked in git (see `.gitignore`).
4. Visit ora-retreats.com to confirm it's live.

## Assets

- `images/logo-primary.png` — the real "ora" wordmark, background removed.
- `images/hero.jpg`, `images/about-portrait.jpg`, `images/moodboard-01.jpg`...`moodboard-13.jpg` —
  real photos, downscaled to a 1600px max edge and recompressed for web (the
  originals in `Tommy/` are far larger and not meant to be served directly).
- `images/retreat-program.jpg` — still a placeholder; swap in the real program
  overview graphic/PDF export when it's ready, keeping the same filename.
