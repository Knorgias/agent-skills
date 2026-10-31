---
name: fe-codebase-overview
description: Write an Overview of a front-end codebase (single package or monorepo) as numbered Markdown files under `overview/` directories. Use when the user asks to understand, map, or onboard onto a front-end repo, or asks for an overview of one.
---

Write an **Overview** of a front-end repo: a map for a developer new to it, who must be able to run it, locate where a change goes, and ship a small safe change. The Overview is a draft until a human has checked its **Evidence**.

## Terms

- **Level**: the repo root, or one package inside a workspace. A single-package repo has only a root level.
- **Section**: one numbered topic, written as one file. Sections and their per-level applicability are in [SECTIONS.md](SECTIONS.md), which also says what each Section looks for and where.
- **Evidence**: the file, config, or command that backs a claim. A claim without Evidence is marked `unverified`.

## Rules for every file

- Every claim carries Evidence. Cite it as a path (`vitest.config.ts`) or a command as written in config (`npm test`, from `package.json`).
- A Section that finds nothing says `none found: <what was searched>`.
- Only write files under `overview/` directories. Source files, config, and git history stay as found, and install/build/dev/test commands stay unrun. Record commands as written, and mark anything that would need running to confirm as `unverified`.
- Leave everything uncommitted.
- Follow [TEMPLATE.md](TEMPLATE.md) for the shape of each file.

## Steps

1. **Survey.** Detect single-package or workspace (workspace field in the root `package.json`, `pnpm-workspace.yaml`, `lerna.json`, `nx.json`, `turbo.json`). List the packages. Read the root config: workspace file, root `package.json`, CI, git hooks, lint/format/type configs. Done when every package path is listed and every root-level file that configures tooling is read.
2. **Existing output.** For each target `overview/` that already exists, read its files. A file whose header commit equals HEAD is skipped. The rest are regenerated in the following steps; a line a human edited that conflicts with the regenerated content keeps the human version and is flagged in the README review list. Done when every existing file is classified skip or regenerate.
3. **Root.** Write the root-level Sections (see SECTIONS.md) into `overview/` at the repo root, plus `overview/README.md`. Done when every root-applicable Section has a file.
4. **Packages.** Skip for a single-package repo, whose root also takes the package-only Sections in step 3. For a workspace, dispatch one subagent per package, in parallel. Each brief contains: the package path, the absolute path of this skill directory, the instruction to read SECTIONS.md and TEMPLATE.md there, the package-level Section list, a summary of the root findings (package manager, workspace tool, shared configs, CI), and the rule to write only inside `<package>/overview/`. Without subagents, work the packages one at a time in the same order, applying the same brief to each: read SECTIONS.md and TEMPLATE.md once, write a package's whole `overview/` before opening the next package, and carry only the root findings plus a one-line note per finished package. Done when every package has a report (subagents) or a completed `overview/` (sequential).
5. **Index.** Fill `overview/README.md` at root: one line per Section file, a link to each package's `overview/README.md`, and a review list at the top naming every `unverified` and `none found` item with its file. Done when every Section file and every package README is linked and every flagged item is listed.

Finish by telling the user the files are uncommitted and the review list is at the top of the root `overview/README.md`.
