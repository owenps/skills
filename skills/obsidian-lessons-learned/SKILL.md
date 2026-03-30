---
name: lessons-learned
description: Run at the end of a dev session to produce a structured summary of lessons learned, decisions made, and suggested vault updates. Use when wrapping up work or when asked to summarize what was learned.
---

# Lessons Learned

Review the current session's work and produce a structured lessons-learned summary for the knowledge base.
This output will be pasted into the Obsidian vault Claude instance for integration.

## Output Format

Use the following format:

```md
# Lessons Learned — [brief description of what was worked on]
Date: [today's date]
Repo: [repo name]
PR: [PR link]

## Decisions made
- [What was decided and why. Focus on the *reasoning*, not the code.]

## Things learned
- [Surprising behaviors, gotchas, patterns that worked, corrections to prior assumptions]

## Suggested vault updates
- **[note topic]**: [what to add or revise, and why]
```

## Instructions

1. Review the conversation history for this session
2. Extract decisions, surprises, and learnings — not implementation details that live in the code
3. For "suggested vault updates", think about what knowledge would have been useful at the *start* of this session — that's what belongs in the vault
4. Keep it concise. A few strong entries beat many weak ones
