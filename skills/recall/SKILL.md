---
name: recall
description: Search the commonplace knowledge base for notes relevant to the current work. Use when starting a task, making an architectural decision, or needing context from past learnings.
---

# Recall

Search the commonplace for knowledge relevant to the current context.

## Instructions

1. Determine what to search for:
   - If `$ARGUMENTS` is provided, use it as the search query
   - If no arguments, infer relevant topics from the current conversation (repo, task, technologies involved)

2. Search `~/Documents/Notes/commonplace/` in two passes:
   - **Filenames** — scan note titles for topic matches
   - **Content** — grep note bodies for keywords related to the query

3. Read any matching notes in full

4. Search index notes (files ending in `Index.md`) for wikilinks to notes that may be relevant but didn't match directly

5. Present findings concisely:
   - Quote the relevant parts, not entire notes
   - Note which commonplace entries are related and why
   - If nothing relevant was found, say so — don't fabricate context

6. Do not modify any vault files. This skill is read-only.
