# HOTIS Projects — Student Field Manual

Documentation site for the Raspberry Pi AI + motor labs (HOTIS program).

Built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/).

## Setup

```bash
pip install -r requirements.txt
```

## Local preview

```bash
mkdocs serve
```

Then open <http://127.0.0.1:8000> in your browser. The site hot-reloads as you edit.

## Deploy

Push to `main`. GitHub Actions builds and publishes to GitHub Pages automatically.

Before the first deploy:

1. Update `site_url` in `mkdocs.yml` with your actual GitHub username.
2. In the repo Settings → Pages, set the source to **GitHub Actions**.

## Source documents

The original lab handouts and wiring diagram live in `_source/` (not published to the site).
