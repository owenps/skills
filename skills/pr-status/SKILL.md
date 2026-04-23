---
name: pr-status
description: Morning PR dashboard for ledgelabs. Shows authored PRs needing attention and PRs awaiting your review. Use to start the day or check in on open work.
allowed-tools: Bash
---

# PR Status

Show a clean dashboard of open PRs across the `ledgelabs` GitHub org.

## CRITICAL: Only ONE Bash call

You MUST use exactly ONE Bash tool call for this entire skill. No additional Bash calls for parsing, grepping, or processing. Run the script below, read the output, then render the dashboard entirely from memory. Do NOT run any follow-up commands.

## Instructions

1. Run this single script:

```bash
authored=$(gh search prs --author @me --state open --owner ledgelabs --json repository,number,title,url,updatedAt,isDraft --limit 30 2>/dev/null)
authored_filtered=$(echo "$authored" | jq -c '[.[] | select(.isDraft == false)]')
echo "=== AUTHORED ==="
echo "$authored_filtered"
reviews=$(gh search prs --review-requested @me --state open --owner ledgelabs --json repository,number,title,url,updatedAt --limit 30 2>/dev/null)
echo "=== REVIEW_REQUESTED ==="
echo "$reviews"
echo "=== DETAILS ==="
all_prs=$(echo "${authored_filtered}${reviews}" | jq -r '.[] | "\(.repository.nameWithOwner // "ledgelabs/\(.repository.name)") \(.number)"' | sort -u)
while read -r repo number; do
  [ -z "$repo" ] && continue
  echo "--- $repo#$number ---"
  gh pr view "$number" --repo "$repo" --json reviewDecision,reviews,statusCheckRollup,isDraft,additions,deletions,author 2>/dev/null | jq '{reviewDecision, isDraft, additions, deletions, author: .author.login, reviews: [.reviews[] | select(.author.login | test("bot|coderabbit|devin"; "i") | not) | {author: .author.login, state: .state}], checks: [.statusCheckRollup[] | {name: .name, conclusion: .conclusion, status: .status}]}'
done <<< "$all_prs"
```

2. After receiving the output, process everything in your head. Do NOT run additional bash commands. Determine status for each PR:
   - FAILING -- any check conclusion is not SUCCESS/NEUTRAL/SKIPPED
   - CHANGES REQUESTED -- a human reviewer requested changes
   - APPROVED -- all human reviewers approved
   - WAITING -- no human reviews yet, or only comments

3. For review-requested PRs, determine urgency from updatedAt.

4. Render the dashboard as plain text output.

## Output Format

Output plain text only. No markdown. No bold, italic, backticks, headers, or code blocks. Plain ASCII characters and whitespace only.

PR STATUS  {date}
----------------------------------------

YOUR PRS
----------------------------------------
[{icon}] {repo}#{number} -- {title}
    {status} | +{adds}/-{dels} | {time since update}
    > {actionable next step}

NEEDS YOUR REVIEW
----------------------------------------
[{icon}] {repo}#{number} -- {title}
    {waiting time} | +{adds}/-{dels}
    > {note if you've already commented}

----------------------------------------
{total authored} open | {total review} awaiting review

Status icons:
  [+] Approved
  [!] Changes requested
  [x] Failing checks
  [~] Waiting for review

Urgency icons:
  [!!] Over 48h
  [!]  Over 24h
  [~]  Under 24h

Rules:
- Sort authored PRs: failing, changes requested, waiting, approved
- Sort review requests: oldest first
- Zero PRs in a section: show "None"
- Truncate titles over 60 chars with "..."
- Actionable steps must be specific: "address review from {name}", "checks passing -- ready to merge", "waiting on {name}"
- Relative times: "2h ago", "1d ago", "3d ago"
- No emoji, no markdown, no unicode -- plain ASCII only
