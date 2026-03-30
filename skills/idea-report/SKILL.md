---
name: idea-report
description: "I have a few spare hours of focus time - what should I work on?"
---

# Idea Report

Give the user a prioritized list of 5 tasks that they should focus on, drawn from real sources.

If a suggested task is too long, suggest a smaller subunit to complete in this session.

## Sources

Gather context from these before generating suggestions:

1. **Polaris** — read `~/Documents/Notes/polaris/` to understand the user's goals and growth direction. Prioritize suggestions that align.
2. **GitHub issues** — run `gh search issues --assignee=@me --state=open --limit=20` to find assigned work across repos.
3. **Zibaldone** — scan `~/Documents/Notes/zibaldone/` for recent entries that hint at unfinished thinking or unexplored ideas.
4. **Commonplace** — scan `~/Documents/Notes/commonplace/` for thin notes or gaps that could be expanded with focused learning.

## Instructions

1. Read all sources above
2. Rank by: alignment with polaris goals > urgency of assigned issues > ripeness of unfinished ideas > knowledge gaps
3. Mix sources — don't just list 5 GitHub issues. A good report blends dev work, learning, and personal growth.
4. For each suggestion, note which source it came from

## Output Format

```md
**Idea Report**

**{idea 1 header}**
{source} — {description and why it's worth doing now}

**{idea 2 header}**
{source} — {description and why it's worth doing now}

...
```
