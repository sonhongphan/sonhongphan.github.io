# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A personal academic website (for Phan Hong Son, deployed at https://sonhongphan.github.io) built on the **Academic Pages** Jekyll template, itself a fork of the Minimal Mistakes theme. It is a static Jekyll site published via GitHub Pages — there is no test suite or linter.

## Commands

```bash
# Install Ruby dependencies (if permission errors: bundle config set --local path 'vendor/bundle')
bundle install

# Serve locally at localhost:4000 with live reload
bundle exec jekyll serve -l -H localhost

# Or run everything in Docker (uses _config_docker.yml)
docker compose up

# Rebuild minified JS after editing files in assets/js/
npm run build:js        # or npm run watch:js to rebuild on change
```

Changes to Markdown/HTML files hot-reload; changes to `_config.yml` require restarting the Jekyll server.

JavaScript: edit `assets/js/_main.js` or `assets/js/plugins/*`, then run `npm run build:js` — never edit `assets/js/main.min.js` directly (it's the uglified bundle of jQuery, fitvids, plotly, and the local scripts).

## Architecture

**Content lives in Jekyll collections** — Markdown files with YAML front matter, one file per item:
- `_publications/`, `_talks/`, `_teaching/`, `_portfolio/`, `_posts/` — each rendered by list pages in `_pages/` (e.g. `_pages/publications.html`, `_pages/talks.html`)
- `_pages/` — standalone pages (about, CV, sitemap, archives); navigation is controlled by `_data/navigation.yml`
- Site-wide identity, author sidebar links, and theme selection live in `_config.yml`

**Theme internals**: `_layouts/`, `_includes/`, and `_sass/` hold the Minimal Mistakes-derived templates and styles. `_data/ui-text.yml` holds localized UI strings.

**Generated content pipelines** (multiple files cooperate; know these before editing outputs by hand):

1. **Talk map** — `talkmap.ipynb` / `talkmap.py` scrape the `location` front-matter field from every file in `_talks/`, geocode it (geopy/Nominatim + getorg), and write the Leaflet cluster map into `talkmap/`, displayed by `_pages/talkmap.html`. The GitHub Action `.github/workflows/scrape_talks.yml` runs this automatically on any push touching `_talks/` and commits the result — so `talkmap/` and `talkmap_out.ipynb` are generated artifacts, not hand-edited files.

2. **CV** — the canonical CV is `_pages/cv.md`. `scripts/update_cv_json.sh` runs `scripts/cv_markdown_to_json.py` to regenerate `_data/cv.json`, which backs the JSON CV page (`_pages/cv-json.md`). Edit `cv.md`, then regenerate — don't edit `cv.json` directly.

3. **Publications/talks generators** — `markdown_generator/` contains notebooks and scripts (`publications.py`, `talks.py`, `PubsFromBib.ipynb`, etc.) that generate collection Markdown files from TSV/CSV or BibTeX sources. These are convenience tools; the generated files in `_publications/` and `_talks/` are what the site actually builds from.
