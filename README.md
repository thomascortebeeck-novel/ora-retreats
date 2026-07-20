# ora-retreats.com

Static marketing site for ora retreats. No build step required.

## Local preview

Open `index.html` directly in a browser, or serve the folder with any static
file server (e.g. `python -m http.server` from this directory).

## Deploying to easyhost.be

1. Log in to the easyhost.be control panel.
2. Open the file manager (or connect via FTP) for the `ora-retreats.com` hosting product.
3. Upload the entire contents of this folder (`index.html`, `moodboard.html`,
   `css/`, `js/`, `images/`) to the web root.
4. Visit ora-retreats.com to confirm it's live.

## Swapping in real assets

- Replace files in `images/` with the real photos, keeping the same filenames
  (`hero.jpg`, `retreat-program.jpg`, `about-portrait.jpg`,
  `moodboard-01.jpg`...`moodboard-08.jpg`) — no HTML changes required.
- Replace the Google Fonts `<link>` in both HTML files if the real logo font
  or title font changes.
