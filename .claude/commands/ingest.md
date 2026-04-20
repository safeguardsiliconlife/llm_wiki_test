---
description: Ingest a source into the wiki. Accepts a file path or pasted text.
---

# Ingest

Integrate a new source into the wiki. Follow the Ingest Workflow defined in CLAUDE.md exactly.

## Usage

```
/ingest path/to/file.md
/ingest
[paste text directly after invoking]
```

## Steps

1. Read `/home/ritsu/code/llm_wiki_test/CLAUDE.md` for schema conventions
2. Determine the source:
   - If an argument was provided, read that file from disk
   - If no argument, the text following the command invocation is the source content
3. Follow the **Ingest Workflow** in CLAUDE.md step by step
4. All wiki writes go to `/home/ritsu/code/llm_wiki_test/wiki/`
5. Use today's date (check with `date +%Y-%m-%d`) for `created`, `updated`, and log entries

## Notes

- Snippets (todos, reminders, short notes) get type: `snippet`
- Longer source documents (articles, notes) get type: `summary`
- Always create or update concept/entity pages for key topics in the source
- Never skip updating `index.md` and `log.md`
