---
name: distill
description: Process zibaldone entries into commonplace notes — expanding existing notes, creating new ones, or aggregating across topics. Use when the user wants to refine raw thoughts into structured knowledge.
---

# Distill

Process zibaldone entries into the commonplace.

## Instructions

1. Read the zibaldone file(s) specified by `$ARGUMENTS` from `~/Documents/Notes/zibaldone/`. If no arguments given, scan recent zibaldone files for unprocessed entries.
2. For each entry, determine if it:
   - **Expands** an existing commonplace note — search for related notes and append/revise
   - **Aggregates** across multiple entries into a new commonplace note — when several entries converge on a theme that doesn't have a note yet
   - **Doesn't warrant a note yet** — some thoughts need to stay raw. Skip these.
3. Follow the vault conventions in AGENTS.md for creating or updating notes.
4. Present a plan before making changes: list which entries map to which notes (new or existing) and why. Wait for approval.
5. After distilling, do not delete or modify the zibaldone entries — they are the original record.
