# File template

Every Section file has this shape. File names are `NN-<slug>.md` from [SECTIONS.md](SECTIONS.md); the same Section has the same number at every Level.

```md
<!-- level: <root | package name> · generated: <YYYY-MM-DD> · commit: <short hash at HEAD> -->

# <NN> <Section title>

## Summary

<2 to 5 lines answering the Section's one question, written for a developer who must ship a small safe change.>

## Details

<The body. Tables and mermaid diagrams belong here when they explain better than prose.>

## Evidence

- <claim> — `<path or command>`
- <claim> — `unverified`: <why it could not be confirmed without running something>

## Not found

- none found: <what was searched>
```

- `## Not found` lists what the Section expects but the repo lacks. When nothing is missing, write `- nothing missing`.
- Mermaid goes in a fenced `mermaid` block inside Details. `03-architecture.md` always has one.
- The README (`overview/README.md`) has the same header comment, a review list, then one line per Section file.
