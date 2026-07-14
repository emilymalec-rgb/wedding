# Emily & Bruce Wedding Site

A single-page wedding website — January 29, 2027, Boracay, Philippines.

## Running it
It's a static site. No build step. Either:
- Open `index.html` directly in a browser, or
- Serve the folder: `python3 -m http.server` then visit `http://localhost:8000`

## Structure
- `index.html` — the entire site (HTML, CSS, and JS are all inline in this one file)
- `assets/` — all images (compressed for web)
  - `hero.jpg`, `story.jpg`, `schedule.jpg`, `travel.png`, `gallery-bg.jpg`
  - `gallery/` — photo gallery images (clickable, open in a lightbox)
  - `story/<year>/` — "Our Story" timeline photos, grouped by year
  - `dress/` — dress-code reference images

## How it works
- Client-side "pages" (Home, Schedule, Our Story, Travel & Stay, Gallery, RSVP, Registry, FAQ) are all in `index.html` as `.page` divs, switched by the `showPage(name)` JS function — no routing library.
- Key JS functions in the `<script>` at the bottom of `index.html`:
  - `showPage(name)` — nav between sections
  - `startCountdown()` — countdown to the wedding date
  - `buildGallery()` — builds the gallery grid + lightbox
  - `initReveal()` — scroll-reveal animations
- Fonts load from Google Fonts (needs internet).

## Notes for editing
- Fonts, colors, and spacing are defined as CSS custom properties in the `:root` block near the top of `index.html`.
- The Gallery photos open a lightbox on click; the Our Story timeline photos are intentionally NOT clickable.
- There is no password gate — the site loads straight to content.

## Deploying
This is a static site — `index.html` + the `assets/` folder are all that ship. Any static host works. Keep the entry file named `index.html`.

- **Cloudflare Pages** — connect this GitHub repo. Framework preset: **None**. Build command: *(leave empty)*. Build output directory: **/** (repo root).
- **Railway** — deploy from this GitHub repo as a static site. No build step; serve the repo root. If Railway asks for a start command, use a static file server, e.g. `npx --yes serve -l $PORT .`.
- **GitHub Pages** — Settings → Pages → deploy from branch `main`, folder `/ (root)`.
- **Netlify / Vercel** — import the repo; build command empty, publish/output directory = repo root.

Custom domain (Cloudflare/Railway): point the domain at the host per the platform's docs; no code changes are needed here.

Note: the `assets/story/` photos are full-resolution PNGs (~118 MB total). They work as-is, but compressing them would speed up page loads for guests on mobile.
