# SUPERHUB

A personal media hub — browse, favourite, and launch streaming sites from a single dark-mode dashboard. Built as a single `index.html` file with no build step required.

Hebrew-first, with a full English language toggle. Works on desktop and mobile.

---

## How it works

SuperHub fetches two plain-text files from this repository at runtime:

- **`Sites.txt`** — the list of sites to display
- **`Credits.txt`** — version and author info shown on the Credits screen

Both files are cached in `localStorage` for 10 minutes, so the page loads instantly on repeat visits.

---

## Sites.txt format

Each line defines one site entry using this format:

```
Name:"URL":Category:subtitles
```

| Field | Description |
|---|---|
| `Name` | Display name shown on the card |
| `URL` | Full URL in double quotes. `https://` is added automatically if missing |
| `Category` | Groups sites into sidebar categories (e.g. `Movies`, `Anime`) |
| `subtitles` | One of `yes`, `mostly`, `rare`, or `no` — shown as a badge on each card |

### Example

```
123Movies:"https://ww8.123moviesfree.net":Movies:rare
AniWatch:"https://aniwatchtv.to":Anime:no
HiMovies:"https://himovies.sx/home":TVShows:mostly
```

- Lines that don't contain a colon are ignored
- Lines without a quoted URL are ignored
- Duplicate category names are deduplicated automatically
- Categories appear in the sidebar in the order they first appear in the file

---

## Credits.txt format

Three keys, one per line:

```
ver:1.5
sentence: כל הזכויות שמורות לאיתמר קצובר
credits: נוצר ע"י איתמר קצובר
```

| Key | Description |
|---|---|
| `ver` | Version string displayed on the Credits screen |
| `sentence` | Rights / copyright line (shown in large italic text) |
| `credits` | Author name |

---

## Features

- **Categories** — auto-generated from `Sites.txt`, no config needed
- **Favourites** — star any site; persists across sessions via `localStorage`
- **Recents** — last 12 visited sites, with a one-tap clear button
- **Search** — filters the current category by name or URL
- **Language toggle** — switches all UI text between Hebrew (RTL) and English (LTR)
- **Iframe overlay** — opens sites inside the app; detects X-Frame-Options blocks and offers "Open in new tab" as a fallback
- **Offline detection** — shows a clear error state if the network is unavailable

---

## Running locally

No build step, no dependencies to install. Just open `index.html` in a browser.

```bash
# Clone the repo
git clone https://github.com/Katzover/SuperHub.git
cd SuperHub

# Open directly — works in any modern browser
open index.html
```

> **Note:** Some browsers block cross-origin fetches from `file://` URLs. If the site list doesn't load, serve it over HTTP instead:
> ```bash
> npx serve .
> # or
> python3 -m http.server 8080
> ```

---

## Updating sites

1. Edit `Sites.txt` directly on GitHub (or clone, edit, push)
2. The next time any user opens SuperHub after the 10-minute cache expires, they'll get the updated list automatically — no redeployment needed

---

## Project structure

```
SuperHub/
├── index.html          # The entire app
├── Sites.txt           # Site list (edit this to add/remove sites)
├── Credits.txt         # Version and author info
├── site.webmanifest    # PWA manifest
├── favicon.ico
├── favicon-16x16.png
├── favicon-32x32.png
├── android-chrome-192x192.png
├── android-chrome-512x512.png
├── apple-touch-icon.png
└── README.md
```

---

## Tech stack

| Thing | What it is |
|---|---|
| React 18 | UI rendering (loaded via CDN, no build step) |
| Babel Standalone | In-browser JSX transpilation |
| Tailwind CSS | Utility-class styling (CDN) |
| Google Fonts | Assistant + Inter |
| localStorage | Favourites, recents, language preference, data cache |

---

*Created by איתמר קצובר · כל הזכויות שמורות*
