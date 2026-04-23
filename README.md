# Skills

A collection of skills for AI coding agents. Skills are packaged instructions and
scripts that extend agent capabilities.

Skills follow the [Agent Skills](https://agentskills.io/) format.

> [!NOTE]
> Various skills are customize to me with hard coded paths, etc.

## Available Skills

### `idea-report`

Pretty much the following quote formalized into a skill:

> *"I have a few hours of spare focus time - what should I work on?"*

Credit to [@jameesy](https://x.com/jameesy)

### `lessons-learned`

Run at the end of a dev session to write learnings directly into the zibaldone — raw, unstructured capture of decisions, surprises, and reasoning.

### `distill`

Process zibaldone entries into commonplace notes — expanding existing notes, creating new ones, or aggregating across topics.

### `pr-status`

Morning PR dashboard. Shows authored PRs needing attention and PRs awaiting your review across a GitHub org.

### `pr-create`

Create a pull request against `main`. Auto-commits uncommitted changes, pushes the branch with upstream tracking, infers a conventional-commit title from the diff, and writes a Summary + Test plan body.

### `recall`

Search the commonplace knowledge base for notes relevant to the current work. Use when starting a task, making an architectural decision, or needing context from past learnings.

## Installation

Fetch the latest with

```bash
npx skills add owenps/skills
```

or to setup a specific skill use `--skill {skill_name}`

```bash
npx skills add owenps/skills --skill idea-report
```

## Usage

Skills are automatically available once installed. The agent will use them when
relevant tasks are detected.

In Claude, skills can also be manually triggered with,

```txt
/{skill_name}
```
