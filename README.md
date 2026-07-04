# Portfolio — Alinda Byamukama

Personal portfolio site. A single, zero-build `index.html` positioning me as a data analyst working toward data engineering, with cloud (GCP) as the foundation.

## Overview

Static site, no framework, no build step. Everything — markup, styles, and the small amount of JavaScript — lives in one `index.html`. It ships as-is to GitHub Pages.

The page is a landing-first, multi-view layout: only the home view renders on load, and the nav (plus the home cards) switch between four views without a page reload.

## Tech

- Plain HTML / CSS / JavaScript — no framework, no bundler, no dependencies to install
- Google Fonts: Fraunces (display), DM Sans (body), JetBrains Mono (labels/mono)
- Client-side **hash routing** for view switching (`#home`, `#projects`, `#resume`, `#contact`)

## Structure

```
.
├── index.html            # the entire site
├── README.md
└── assets/
    ├── profile_ab_3-round.png
    ├── CV.pdf
    └── favicon.png
```

Inside `index.html`:

- **Views** — four `<section class="view" data-view="...">` blocks. All but the active one carry the `hidden` attribute. A tiny router reads `location.hash` and toggles which view shows, updates the active nav link, and scrolls to top.
- **Nav** — a persistent top bar. On mobile (≤640px) it collapses to a hamburger toggle (`.nav-toggle` / `.nav-links.open`), which is `aria-expanded`-wired.
- **Motion** — the active view fades in via a `.entering` class; `prefers-reduced-motion` disables it.
- **Home cards** — the three nav tiles use per-corner `border-radius` (a different asymmetric value per card) for a leaf/pebble shape that settles to an even round on hover.

### Design tokens

Defined as CSS variables in `:root` — change them there and the whole site follows.

| Token | Value | Role |
|-------|-------|------|
| `--bg` | `#FBF8F3` | warm off-white background |
| `--ink` | `#221D17` | primary text |
| `--muted` | `#6F6659` | secondary text |
| `--accent` | `#A8442A` | deep terracotta accent |
| `--card` | `#F2ECE2` | card fill |
| `--line` | `#E6DECF` | borders / rules |

## Run locally

No build. Either open the file directly:

```
open index.html
```

…or, to test hash routing under a real server:

```
python -m http.server 8000
# then visit http://localhost:8000
```

## Deploy (GitHub Pages)

On a free personal account, **the repo must be public** — GitHub Pages does not publish from private repos without a paid plan.

1. Push this repo to GitHub (public).
2. Settings → Pages → Build and deployment → Source: **Deploy from a branch**.
3. Branch: `main`, folder: `/ (root)`. Save.
4. Wait a few minutes, then visit the URL Pages shows you.

## Customize before publishing

A few values are placeholders and must be set to real ones:

- **Open Graph URL + image** (`<head>`): `og:url` and `og:image` point at `alindabyamukama.com`. If the live site is actually a `github.io` URL, change both — and remember `og:image` needs an **absolute** URL, not a relative `assets/…` path.
- **Project links**: several `Source ↗` links are `#` placeholders. Fill or remove them; a dead link reads worse than none.
- **`assets/CV.pdf`**: make sure the current CV is in place (phone number removed).

## Notes

- The page carries `<meta name="robots" content="noindex, nofollow">` — it stays out of search engines but remains reachable by direct link. This does **not** block LinkedIn/Twitter link previews, which read the OG tags directly.
- The blog link points to `https://alindabyamukama.hashnode.dev/` in both the nav and the hero.

## License

No license.