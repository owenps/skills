---
name: pr-create
description: Create a pull request against main. Auto-commits uncommitted changes, pushes the branch with upstream tracking, infers a conventional-commit title from the diff, and writes a Summary + Test plan body. Use when wrapping up work and ready to open a PR.
allowed-tools: Bash
---

# PR Create

Create a pull request against `main` for the current branch.

## Instructions

1. Check repo state with a single parallel batch:
   - `git status --porcelain`
   - `git branch --show-current`
   - `git diff main...HEAD --stat`
   - `git log main..HEAD --oneline`

2. Guard against bad states — report error to the user and stop if any apply:
   - Current branch is `main` (refuse: "Cannot create PR from main")
   - No commits ahead of `main` AND no uncommitted changes (refuse: "No changes to PR")
   - Branch is already pushed and diverged from its upstream (report the divergence and stop — do not force-push)

3. If there are uncommitted changes (tracked modifications or untracked files you can identify as part of the work), auto-commit them:
   - Stage specific files by name (never `git add -A` or `git add .` — avoid sweeping in secrets/junk)
   - Skip files that look like secrets (`.env*`, `*credentials*`, `*.pem`, `*.key`) — warn the user if you see any
   - Write a conventional-commit message inferred from the diff
   - Commit with a HEREDOC message

4. Push the branch with upstream tracking if not already pushed:
   - `git push -u origin <branch>`
   - If already pushed and up-to-date with upstream, just `git push`

5. Infer the PR title from the full diff (`git diff main...HEAD`) and commit history:
   - Use one of: `feat:`, `fix:`, `refactor:`
     - `feat:` — new capability, new endpoint, new user-visible behavior
     - `fix:` — bug fix, incorrect behavior corrected
     - `refactor:` — restructuring without behavior change (renames, extractions, cleanup)
   - Keep title under 70 characters
   - Don't cram details into the title — put them in the body

6. Write the PR body with this structure:

   ```markdown
   ## Summary
   - <what changed, why it changed — 1-3 bullets>

   ## Test plan
   - [ ] <specific, checkable test step>
   - [ ] <another test step>
   ```

   - Summary bullets focus on the *why*, not a file-by-file recap
   - Test plan items should be things a reviewer or you can actually run/verify — not vague ("tested it works")

7. Create the PR:
   ```bash
   gh pr create --base main --title "<title>" --body "$(cat <<'EOF'
   <body>
   EOF
   )"
   ```

8. Print the PR URL returned by `gh pr create`. Nothing else.

## Rules

- Never force-push. Never `--no-verify`. Never skip hooks.
- Never assign reviewers or labels.
- Default to ready-for-review (not draft).
- Always target `main` as the base.
- If `gh pr create` fails, report the error verbatim and stop — don't retry with different flags.
