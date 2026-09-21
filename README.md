# hyperion-git.github.io

Personal website of Alexander Friedrich — <https://hyperion-git.github.io/>.

Built with [al-folio](https://github.com/alshedivat/al-folio) v1.x (Jekyll). The al-folio starter is tracked as the `upstream` remote so that
theme releases can be merged in.

## Layout

- `_pages/` — about, publications, projects, notes, blog
- `_bibliography/papers.bib` — publication list (rendered by jekyll-scholar)
- `_projects/` — project cards
- `_notes/` — short technical notes (collection listed at `/notes/`)
- `_posts/` — blog posts (`YYYY-MM-DD-title.md`)
- `_data/socials.yml` — profile links

## Local preview

```bash
docker compose up -d          # http://127.0.0.1:8080/
docker compose logs -f
docker compose down
```

Edits to `_config.yml` restart the Jekyll server inside the container; everything else hot-reloads.

## Deployment

`.github/workflows/deploy.yml` builds the site on every push to `main` and publishes it to the `gh-pages` branch, which GitHub Pages serves.

## Upgrading al-folio

```bash
git fetch --tags upstream
git merge v1.x            # resolve conflicts in _config.yml / Gemfile if any
```

Content and configuration live in this repo; layouts, includes and styles come from the `al_folio_*` gems pinned in the `Gemfile`.
