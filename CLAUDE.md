# Wiki Schema

This is a personal LLM-maintained wiki. You (Claude) write and maintain all files in `wiki/`. The user curates sources and asks questions. You do the bookkeeping.

## Directory Layout

```
raw/          # Immutable source documents. Never modify these.
  images/     # All images (Obsidian attachment target)
  (flat)      # All other source files live directly in raw/
wiki/         # Your domain. All LLM-generated pages live here.
  index.md    # Content catalog. Update on every ingest.
  log.md      # Append-only operation log. Append on every operation.
```

**raw/ rules:**
- Images always go in `raw/images/`
- Text files (articles, clipped pages, notes) live flat in `raw/`
- Pasted text snippets are ephemeral — do not save them to `raw/`; the wiki page is the artifact

## Wiki Page Format

Every page in `wiki/` (except `index.md` and `log.md`) uses this structure:

```markdown
---
title: Page Title
type: concept | entity | summary | synthesis | snippet
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [source-filename-or-description]
---

# Page Title

[Content]

## Related
- [[Other Page]]
```

**Page types:**
- `concept` — an idea, topic, or domain (e.g. "Attention Mechanisms", "Sleep Hygiene")
- `entity` — a specific person, place, project, tool, or book
- `summary` — distillation of a specific source document
- `synthesis` — answer to a query or cross-source analysis, filed from a /query result
- `snippet` — a short note, todo, reminder, or text fragment with no specific source

## index.md Format

Organized by type. Each entry: `- [[Page Title]] — one-line description`

```markdown
# Wiki Index

## Concepts
- [[Page Title]] — one-line description

## Entities
## Summaries
## Syntheses
## Snippets
```

## log.md Format

Append-only. Each entry header: `## [YYYY-MM-DD] operation | Title`
Operations: `ingest`, `query`, `lint`

```markdown
## [2026-04-20] ingest | Article Title
Brief note on what was added or changed.
```

## Ingest Workflow

When `/ingest` is invoked:

1. Read this file (CLAUDE.md) first for conventions
2. Determine the source:
   - If a file path was given, use that
   - If no argument, run `git status` to find untracked files in `raw/` and offer to ingest them
   - If pasted text, treat as an inline snippet (no raw file)
3. Briefly summarize key takeaways to the user (2-3 sentences), confirm emphasis
4. Determine what pages to create or update
5. Create a `summary` or `snippet` page in `wiki/`
6. Create or update any relevant `concept` or `entity` pages; add cross-links
7. Append an entry to `wiki/log.md`
8. Update `wiki/index.md` with all new/changed pages
9. Commit everything: `git add -A && git commit -m "[YYYY-MM-DD] ingest | <title>"`
10. Report: pages created, pages updated

**Cross-linking rule:** Use `[[Page Title]]` syntax. If a concept is mentioned that doesn't have its own page yet but warrants one, create a stub.

## Query Workflow

When `/query` is invoked:

1. Read this file (CLAUDE.md) first
2. Read `wiki/index.md` to identify relevant pages
3. Read the relevant pages
4. Synthesize an answer with `[[Page]]` citations inline
5. Present the answer
6. Ask the user: "File this as a wiki page? [y/N]"
7. If yes: write a `synthesis` page, update `index.md` and `log.md`

## Lint Workflow

When asked to lint the wiki:

- Flag contradictions between pages
- Identify orphan pages (no inbound links from other pages)
- Identify concepts mentioned but lacking their own page
- Flag stale claims if newer sources contradict them
- Suggest new questions or sources to investigate

## Conventions

- Never modify files in `raw/`
- Always update `index.md` and `log.md` after any write
- Cross-link liberally — connections are the wiki's value
- Keep page titles consistent across all cross-references
- Prefer updating existing pages over creating near-duplicates
