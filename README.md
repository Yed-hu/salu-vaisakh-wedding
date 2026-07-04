# Salu & Vaisakh — Wedding Invitation

A single-page, self-contained digital wedding invitation for **Salu & Vaisakh**, 24 October 2026, at Sree Narayana Auditorium, Ramalakkalmedu, Idukki.

Everything — markup, styling, animation, and RSVP logic — lives in one file: `index.html`. There is no build step and no dependencies to install; it just needs to be opened in a browser or hosted as a static file.

## Features

- **Name gate** — guests type their name before the invitation unlocks; the name is title-cased and carried into the greeting and RSVP form.
- **Hero section** — Sanskrit shloka blessing, couple's names, and a Radha-Krishna motif rendered as a CSS background.
- **Family details** — bride and groom names, parents, and house addresses.
- **Ceremony & Venue** — muhurtham date/time and an embedded Google Map with a "Get Directions" link.
- **Live countdown** — days/hours/minutes/seconds to the ceremony.
- **Photo gallery** — fading carousel slideshow (4 slides, 5s each, 20s loop). Currently commented out in the HTML pending real photos (see Known Issues).
- **RSVP form** — name, house name, phone (with country code), attendance, and guest count. Submits to a Google Apps Script backend, with duplicate-IP and duplicate-phone detection.
- **Ambient details** — falling gold-dust particle animation, scroll-reveal transitions, custom alert modal in place of native `alert()`.
- **Responsive** — mobile layout adjustments below 640px.

## Running it

Just open `index.html` in a browser, or serve the folder with any static file server (e.g. `npx serve`, GitHub Pages, Netlify).

## Configuring for your own event

All content lives directly in the HTML — no CMS or config file. To reuse this for another wedding:

| What | Where |
|---|---|
| Names, date, venue | `<title>`, the `#gate` block, `.hero-names`, `.event` sections, footer |
| Family details | `.families` section |
| Google Map | `iframe src` and the `Get Directions` link in `#venue` |
| Countdown target | `target` date inside `startCountdown()` in the `<script>` |
| RSVP backend | `scriptURL` inside the `rsvp-btn` click handler — points to a Google Apps Script Web App deployment that handles storage + dedup logic |
| Gallery photos | `background-image` in `.slide-1`–`.slide-4` |
| Colors/fonts | CSS custom properties in `:root` (`--primary`, `--secondary`, `--gold-accent`, etc.) |

## Known issues

- The gallery `<section>` is commented out in the HTML (search for `PHOTO GALLERY (FADING CAROUSEL)`) until real photos are ready. To bring it back: replace the `placehold.co` URLs in `.slide-1`–`.slide-4` with real photo URLs, then remove the `<!--` / `-->` wrapping the `<section class="gallery ...">` block.
- The RSVP flow sends the guest's public IP (via `api.ipify.org`) to the backend for duplicate detection — factor this into any privacy messaging for guests.
- The RSVP backend URL is a hardcoded Google Apps Script deployment; if that deployment is redeployed or torn down, the URL will need updating.

## Tech notes

- No framework — vanilla HTML/CSS/JS.
- Fonts (`Inter`, `IBM Plex Mono`, `Cinzel`) are loaded from Google Fonts, so an internet connection is required for correct typography.
- The Ganesha artwork and hero background image are embedded as base64 data URIs, which is why the file is large (~100KB) despite having no external image assets.
