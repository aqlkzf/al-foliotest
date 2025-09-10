# Repository Guidelines

## Project Structure & Module Organization
- Content: `_pages/` (static pages), `_posts/` (blog posts), `_projects/`, `_news/`, `_books/`, `_bibliography/`, `_data/` (YAML).
- Presentation: `_layouts/`, `_includes/`, `_sass/` (styles), `assets/` (images, JS, CSS), `_scripts/` (build helpers).
- Config: `_config.yml` (site settings), `Gemfile*` (Ruby deps), `purgecss.config.js` (CSS pruning).
- Naming: use lowercase-hyphenated filenames. Blog posts: `_posts/YYYY-MM-DD-title.md`.

## Build, Test, and Development Commands
- Install deps (Ruby): `bundle install`
- Local dev (Ruby): `bundle exec jekyll serve --livereload` (opens on `http://localhost:4000`).
- Build site: `bundle exec jekyll build` (outputs to `_site/`). Shortcut: `bin/cibuild`.
- Docker dev: `docker compose up` (serves on `http://localhost:8080`). Use `docker-compose-slim.yml` for lighter image.
- Format Liquid/HTML/Markdown: `npx prettier --write .` (config in `.prettierrc`).
- Pre-commit hooks: `pre-commit install && pre-commit run -a`.

## Coding Style & Naming Conventions
- Indentation: 2 spaces for Liquid/HTML/YAML.
- Liquid/HTML: keep lines under `printWidth` in `.prettierrc` (150). Prefer includes/partials over duplication.
- Front matter: include `layout`, `title`, `date`, and relevant keys (e.g., `categories`, `tags`, `permalink`).
- Assets: place images under `assets/img/…` and reference with relative URLs or site variables.

## Testing Guidelines
- Verify production build: `JEKYLL_ENV=production bundle exec jekyll build` (fail on warnings/errors).
- Optional CSS pruning: `npm i -g purgecss && purgecss -c purgecss.config.js` to mirror CI.
- CI: GitHub Actions builds, purges CSS, and deploys on pushes/PRs touching content/templates.

## Commit & Pull Request Guidelines
- Commits: short, imperative, and scoped (e.g., `pages: update about page`). Group related changes.
- Branches: `feature/<slug>` or `fix/<slug>`.
- PRs: include a clear description, linked issues, and screenshots/GIFs for visual changes. Note any config changes in `_config.yml`.
- Do not commit `_site/` or secrets. Large binaries and generated files are discouraged.

## Security & Configuration Tips
- Keep `_config.yml` and data files minimal and deterministic; avoid embedding secrets/keys.
- For deployment to `gh-pages`, you can use `bin/deploy` (reads from `main` to `gh-pages`).
