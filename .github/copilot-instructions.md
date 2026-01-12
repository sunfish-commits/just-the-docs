Purpose
-------
This file gives succinct, actionable guidance so AI coding agents can be immediately productive in the "Just the Docs" Jekyll theme repository.

Quick start (commands)
- Install Ruby deps: `bundle install` (uses the `Gemfile`).
- Serve site locally: `bundle exec jekyll serve --livereload` (dev server at http://localhost:4000).
- Build for production: `bundle exec jekyll build`.
- Generate search data (uses `lib/tasks/search.rake`): `bundle exec rake search:init` (writes `/assets/js/search-data.json`).
- Run Ruby tests: `bundle exec rspec` (RSpec configured in `Gemfile`).
- Lint/format front-end assets: `npm run lint`, `npm run format` (see `package.json` scripts).

Big-picture architecture
- This repository is a Jekyll theme (not a standalone app). Key boundaries:
  - Theme assets/layouts: `_layouts/`, `_includes/`, `_sass/` — these are packaged into the gem.
  - Example site/docs content: `docs/` — contains example pages and the documentation site that uses the theme.
  - Packaging/metadata: `just-the-docs.gemspec`, `Gemfile` define the gem-based distribution.
  - Build/test helpers: `lib/tasks/` (e.g. `search.rake`) and `spec/` contain tests.

Project-specific conventions and patterns
- Gem-based theme: development uses `bundle` and `bundle exec jekyll ...`. When the theme is consumed as a gem, only files tracked in the gemspec (primarily `_layouts`, `_includes`, `_sass`) are included.
- Search data generation: `lib/tasks/search.rake` creates `assets/js/zzzz-search-data.json` with a permalink `/assets/js/search-data.json`. Use `rake search:init` to regenerate search index after content changes.
- Docs defaults: `_config.yml` sets `defaults:` for `path: "docs"` and `layout: default`. Content in `docs/` is served using the theme layouts.
- Mermaid: mermaid is opt-in via `_config.yml` (`mermaid:` block) and configuration in `_includes/mermaid_config.js`.
- Front-end styling: SCSS lives under `_sass/` and compiled assets are in `assets/css/`. Use `npm run lint` and `npm run format` to check/format styles.

Developer workflows (typical tasks and where to look)
- Preview changes while editing theme code: run `bundle exec jekyll serve --livereload` from repo root and edit files in `_layouts/` or `_includes/`.
- Run accessibility and integration tests: specs in `spec/` use RSpec, Capybara, and axe-core (see `Gemfile` development group). Run `bundle exec rspec`.
- Update search behavior: edit `lib/tasks/search.rake` or `docs/` content then run `bundle exec rake search:init`.
- Packaging notes: files excluded from the gem/site are declared in `_config.yml` `exclude:` — be careful when changing packaging-related files (gemspec, Gemfile) because those files are not included in the gem.

Helpful files to inspect (examples)
- `Gemfile` — project dependencies and test gems.
- `_config.yml` — site defaults, `search` options, `mermaid` opt-in and packaging `exclude` list.
- `lib/tasks/search.rake` — search JSON generation logic and permalink mapping.
- `package.json` — lint/format scripts for front-end assets.
- `_layouts/default.html`, `_includes/` — where layout and page composition live.
- `docs/` — example content that demonstrates supported patterns (see `docs/index-test.md` and UI components under `docs/ui-components/`).

What the agent should avoid changing without context
- Modifying `gemspec`, `just-the-docs` packaging, or files listed in `_config.yml` `exclude:` without explicit intent to change gem behavior.
- Changing `_config.yml` keys that affect site generation (e.g., `permalink`, `defaults`, `plugins`) without running a local server to verify.

If unclear or needing more context
- Ask for which workflow to prioritize (theme development, docs authoring, packaging, or accessibility testing) and whether to run CI locally. Include the exact command you will run next.

End of file
