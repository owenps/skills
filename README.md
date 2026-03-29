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
