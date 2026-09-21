# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## This site (overrides the al-folio starter docs below)

This is Alexander Friedrich's personal **user site** built from al-folio v1.x, deployed at `https://hyperion-git.github.io/` — not the al-folio demo.
Where `AGENTS.md` or `docs/` say otherwise, these facts win:

- `baseurl` is **empty** (user site at the domain root). Never set it to `/al-folio`; verify with `curl -fsS http://127.0.0.1:8080/` and build with a plain `bundle exec jekyll build`.
- Content lives in `_pages`, `_bibliography/papers.bib`, `_projects`, `_notes` (custom collection, listed by `_pages/notes.md`), `_posts`, `_data/socials.yml`.
- **No CV on the site** (owner's decision): `al_folio.features.cv.enabled: false`, no `_pages/cv.md`, no `_data/cv.yml`, no `resume.json`, no CV PDF. Do not add personal data beyond professional affiliation — no address, e-mail (unless `protect_email: true` and the owner asks), dates of birth or school history.
- `_bibliography/papers.bib` was built from ORCID 0000-0003-0588-1989 + the owner's JabRef library + Crossref/arXiv. Never hand-type a bib entry; every entry carries a DOI or arXiv id retrieved from a source.
- Only `.github/workflows/deploy.yml` is kept; the al-folio maintainer workflows were removed on purpose. The `test/` integration scripts and visual baselines are upstream tooling and are not run here.
- Remotes: `origin` = hyperion-git/hyperion-git.github.io (commit identity `hyperion-git <hyperion-git@users.noreply.github.com>`, no Signed-off-by), `upstream` = alshedivat/al-folio (merge release tags to upgrade).
- **Layout overrides** (tracked drift points, `bundle exec al-folio upgrade overrides audit`): `_layouts/about.liquid`, `_layouts/page.liquid`, `_layouts/bib.liquid` (badge links to DOI/arXiv), plus the site-local `_layouts/note.liquid` and `_includes/site_profile.liquid` (portrait + icons on every page, image from `profile_image` in `_config.yml`).
- **Design**: Material console greys with the AFP blue `#2E2CB8` as accent (`#8280D4` lifted on the dark ground) and the ClockWerQ type system (Source Sans 3 Light/Semibold, Source Code Pro), self-hosted woff2 in `assets/fonts/` (SIL OFL). All tokens and type rules live in `_sass/_site.scss`, pulled in by the shadowed `assets/css/main.scss` (a copy of the gem's entry plus `@use "site"`). Colours are set as CSS custom properties there — a shadowed `_sass/_variables.scss` does **not** reach gem partials. The font `<link>` slot `third_party_libraries.google_fonts.url.fonts` points at `/assets/css/fonts.css`; keep it self-hosted (owner's decision, GDPR).
- **Affiliations**: none on the site until **2026-12-01**; from that date add ClockWerQ GmbH (CTO) to the about subtitle/`more_info` and the meta description. No DLR mention (owner's decision, 2026-09-21).

@AGENTS.md

`AGENTS.md` (imported above) is the **authoritative** agent entry point: change routing, the stop sign for gem-owned paths, the three silent failure modes, and the validated command set. Keep it short and ecosystem-neutral. Cross-repo architecture — the wrapper/tag/gem delegation table, feature gating, the v1 config contract, local overrides — lives in [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md); area-to-gem ownership lives in [`docs/BOUNDARIES.md`](docs/BOUNDARIES.md).

**Read those three before editing anything.** Everything below is Claude-specific or longer-form operational detail that does not belong in the short entry point. Do not restate facts from those files here — link to them.

## Daily dev loop

```bash
bundle install                                # ruby gems
bundle exec jekyll serve                      # dev server → http://localhost:4000/al-folio/  (NOTE baseurl)
bundle exec jekyll build --baseurl /al-folio  # production-style build to _site/
bash test/integration_distill.sh              # run ONE integration test (any of the seven in test/)
npm run test:visual:update                    # refresh playwright snapshots after intentional UI change
bundle exec al-folio upgrade apply --safe     # deterministic codemods (font-weight-* → font-*, remote→local URLs)
bundle exec al-folio upgrade overrides diff <path>    # then `overrides accept <path>` to acknowledge an override
```

## Optional toolchains

- **Jupyter posts.** `bin/setup-python-deps` installs _only_ `jupyter` and `nbconvert` (via `pip --user --break-system-packages`) for `jekyll-jupyter-notebook`. It does **not** read `requirements.txt`. Missing `jupyter-nbconvert` is warn-and-continue; notebook rendering is skipped.
- **Everything else Python.** [`requirements.txt`](requirements.txt) is the fuller list and must be installed separately (`python3 -m pip install -r requirements.txt`): `rendercv[full]` for CV rendering, `scholarly` for `bin/update_scholar_citations.py`, plus `nbconvert` and `pyyaml`.
- **Responsive images.** `imagemagick.enabled: true` needs ImageMagick `convert` on `PATH`.
- **Manual deploy.** `bin/deploy` is the manual `gh-pages` build + purgecss + force-push path; CI normally deploys. `purgecss` is not a devDependency — install it with `npm install -g purgecss`.

## Docker serving model (v1-specific)

`docker compose up -d` bind-mounts the repo to `/srv/jekyll` and runs `bin/entry_point.sh`, which serves with `--force_polling --destination /tmp/_site`. The build output deliberately goes to **container-local `/tmp/_site`, not the bind-mounted `_site`** — writing `_site` back across the host bind mount caused write deadlocks. The container also `inotifywait`s `_config.yml` and restarts Jekyll on change (config edits aren't hot-reloaded by `--watch`). Verify with the `/al-folio` baseurl: `curl -fsS http://127.0.0.1:8080/al-folio/`. `docker-compose-slim.yml` pulls a prebuilt `:slim` image instead of building locally.

## CI gates and the style contract

`npm run lint:style-contract` (`test/style_contract.js`) is the automated enforcement of the thin-starter boundary and will fail CI if you cross it. Beyond the forbidden paths listed in `AGENTS.md`, it also asserts that `_config.yml` keeps `theme: al_folio_core` and the required plugins, that the `third_party_libraries` SRI pins are present, and that the `al_math` Gemfile pin stays on a released version rather than a git branch.

Other gates:

- `unit-tests.yml` — style contract plus all seven `test/integration_*.sh` scripts (`comments`, `plugin_toggles`, `distill`, `bootstrap_compat`, `upgrade_cli`, `css_minify`, `new_plugins`).
- `visual-regression.yml` — Playwright on chromium + webkit, diffing the candidate build against a `v0.16.3` baseline worktree served on `:4100` via `BASELINE_URL`.
- `upgrade-check.yml` — `bundle exec al-folio upgrade audit`.
- `prettier.yml` — Prettier with `@shopify/prettier-plugin-liquid` and `printWidth: 150`. Run `npm run lint:prettier` before pushing; `npx prettier . --write` fixes.
- `update-tocs.yml` — regenerates `<!--ts-->…<!--te-->` blocks in changed root and `docs/` Markdown files. If you add or rename a heading, expect a follow-up auto-commit on `main`.

## Gem version pins

`Gemfile` pins every `al-*` gem to an exact released version in `group :al_folio_plugins`, and `_config.yml` lists the same gems under `plugins:`. Read the current pins from the `Gemfile` rather than trusting any version quoted in prose — including here. To test a gem fix against this site, repoint the `Gemfile` at a sibling checkout (`path:`, `git:`, or `branch:`) and `bundle install`; see [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md#working-on-a-gem-alongside-the-starter). Revert the pin before committing.
