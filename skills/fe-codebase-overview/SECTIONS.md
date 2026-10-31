# Sections

Ten Sections, in reading order. **Root** and **Package** columns say which Levels write the Section. A single-package repo writes all ten at its root.

| # | File | Root | Package | One question |
|---|---|---|---|---|
| 01 | `01-tool-stack.md` | ✅ | ✅ | What is this built with? |
| 02 | `02-run-locally.md` | ✅ | ✅ | How do I get it running? |
| 03 | `03-architecture.md` | ✅ | ✅ | Where does a change belong? |
| 04 | `04-cross-cutting.md` | | ✅ | How are the common problems solved here? |
| 05 | `05-conventions.md` | ✅ | ✅ | Where does new code go, and how is it written? |
| 06 | `06-quality-gates.md` | ✅ | ✅ | What checks my change? |
| 07 | `07-build-release-workflow.md` | ✅ | ✅ | How does a change reach users? |
| 08 | `08-observability.md` | | ✅ | How do I see a failure in production? |
| 09 | `09-gotchas.md` | ✅ | ✅ | What will surprise me? |
| 10 | `10-domain-vocabulary.md` | ✅ | ✅ | What do the product's own terms mean in code? |

Each Section below lists what differs by Level, then where to look. Every item found becomes a claim with Evidence.

## 01 Tool stack

- Root: package manager (lockfile), workspace tool, Node version pin (`.nvmrc`, `engines`, `.tool-versions`), repo-wide language and TypeScript base config.
- Package: framework, bundler, language/TS config, styling approach, runtime (browser, SSR, edge), key libraries for state, routing, and data fetching. Look in `package.json` dependencies, bundler config, `tsconfig*.json`.

## 02 Run locally

- Root: install command, commands to run everything or filter to one package, required env files, required tools.
- Package: its dev command, which backend the dev server talks to (mock, local, staging; see proxy config and env files), seed or mock data. Look in `package.json` scripts, `README`, `.env*.example`, proxy and mock config.

## 03 Architecture diagram

The **Architecture diagram** is one mermaid picture: the **source map** with the **data flow** drawn over it.

- Root: a mermaid graph of packages and their dependency direction (from workspace dependency fields and import graph), shared packages marked, external systems (backend APIs, auth provider, CDN, analytics, feature flags) listed beneath the diagram.
- Package: a mermaid graph of top-level folders and layers (routes/pages, components, state, data access, utilities) with allowed dependency direction, and the primary data flow over it: user action to state to API client to backend and back, with where state lives. Add the folder-to-responsibility table below the diagram. Look at the `src/` layout, entry points, router config, API client modules, store setup, and lint rules that restrict imports.

## 04 Cross-cutting concerns

Package only. One line each, with a pointer to the canonical example file: routing, state management, data fetching, styling or design system, forms and validation, i18n, accessibility, error handling. Look for the existing implementation closest to the concern, and the library that provides it. A concern with no implementation is `none found`.

## 05 Conventions

- Root: repo-wide rules (commit format, branch naming, file naming, import aliases, formatting config). Look in `CONTRIBUTING.md`, `.editorconfig`, commitlint, root lint config.
- Package: where new components, hooks, utils, and tests go; naming patterns observed across at least three existing files; local exceptions to the root rules.

## 06 Quality gates

A table with one row per check: lint, format, type check, unit tests, integration/e2e tests, git hooks, CI jobs, bundle or size checks, dependency checks. Columns: check, tool, local command, where it also runs (pre-commit, pre-push, CI, or several), config file.

- Root: shared configs, hook runner (`.husky/`, `lefthook.yml`, `simple-git-hooks`), CI workflows (`.github/workflows/`, other CI config).
- Package: its own scripts and config overrides, test runner and setup files, test file location and naming.

## 07 Build, release, change workflow

- Root: CI/CD pipeline stages in order, environments in order (preview, staging, production), versioning and changelog tooling (changesets, semantic-release), branch and PR rules (`CODEOWNERS`, PR template, required checks), how a merge becomes a release. Draw the pipeline as a mermaid diagram when it has more than three stages.
- Package: build command and output directory, environment-specific config (env vars, feature flags: names and where read, not values), and the destination: `publish` (registry, prepublish steps, `files`/`exports`) for a library, `deploy` (host, SSR/static/edge, CDN) for an app.

## 08 Observability

Package only. Error tracking, analytics, logging, performance monitoring, source map upload, and how to find a failure in production. Look for SDK initialisation in the entry point and the related dependencies. Record names and config locations; leave keys and DSNs out.

## 09 Gotchas

- Root: workspace-level surprises (hoisting, version overrides/resolutions, patches, generated files that are committed, tasks that must run in an order).
- Package: surprises local to it. Sources: `TODO`/`FIXME`/`HACK` comments, patch files, lint disables, pinned or overridden dependencies, code-generated files, `README` warnings, comments explaining why something is odd. Each gotcha carries the file where it shows.

## 10 Domain vocabulary

- Root: product terms shared across packages.
- Package: terms local to it. Sources: type and model names in the data layer, route names, API response types, UI copy, any glossary file. Each entry maps a product term to its code name and file. Terms that mean different things in different places are listed once with each meaning.
