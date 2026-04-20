---
description: Query the wiki and synthesize an answer from existing pages.
---

# Query

Answer a question using the wiki's existing knowledge. Follow the Query Workflow in CLAUDE.md exactly.

## Usage

```
/query What do I know about X?
/query Compare X and Y
/query What are my open todos?
```

## Steps

1. Read `/home/ritsu/code/llm_wiki_test/CLAUDE.md` for schema conventions
2. Read `wiki/index.md` to identify relevant pages
3. Read the relevant pages from `wiki/`
4. Follow the **Query Workflow** in CLAUDE.md step by step
5. If filing the result: use today's date (`date +%Y-%m-%d`), type `synthesis`

## Notes

- Cite pages inline using `[[Page Title]]` syntax
- If the answer reveals a gap (concept that should exist but doesn't), mention it
- When filing a synthesis, always update `index.md` and `log.md`
