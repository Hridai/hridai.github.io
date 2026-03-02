# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static personal portfolio website (`hridai.github.io`) based on the [Quicksilver](https://github.com/jacksonhvisuals/quicksilver) template. It is deployed via GitHub Pages with no build process — all files are served directly.

## Development

Since there is no build system, simply open `index.html` in a browser or serve locally:

```bash
# Using Python (available on most systems)
python -m http.server 8000

# Using Node.js npx
npx serve .
```

A local server is required (rather than opening `index.html` directly) because `js/index.js` fetches JSON files via XHR, which browsers block for `file://` URLs.

## Architecture

### Content Data Flow

All dynamic content is driven by two JSON files fetched at runtime via `js/index.js`:

- **`json/links.json`** — Social/contact links rendered in the left profile column. Each entry: `name`, `color`, `icon` (from [materialdesignicons.com](https://materialdesignicons.com), without the `mdi-` prefix), `url`.
- **`json/items.json`** — Portfolio project cards rendered in the right column. Each entry: `name`, `description`, `image` (path relative to root), `link`. Images **must all share exact pixel dimensions** (e.g. 1920×1080) due to MaterializeCSS constraints.

### Layout

`index.html` uses a MaterializeCSS 12-column grid:
- Left column (`col s12 l4`): profile image, name, description, social links, contact button
- Right column (`col s12 m12 l8`): portfolio cards

### Dependencies (all vendored, no npm)

- **MaterializeCSS** (`css/materialize.min.css`, `js/materialize.min.js`) — grid, cards, wave effects
- **Material Design Icons** (`css/materialdesignicons.min.css`) — icons for social links
- **jQuery 3.2.1** — loaded from CDN (`code.jquery.com`)
- **Google Fonts** — Saira Semi Condensed (loaded from CDN)

### Customisation Points

| What to change | Where |
|---|---|
| Name, description, contact email | `index.html` |
| Social links | `json/links.json` |
| Portfolio projects | `json/items.json` |
| Profile photo | `images/profile.jpg` |
| Custom styles | `css/index.css` |
| Page metadata (SEO) | `<head>` in `index.html` |
