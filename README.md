# Claude Code Skills

Personal Claude Code skills library. Contains reusable skill definitions for project planning,
architecture decisions, and development workflows.

## Installation

Clone directly into Claude Code's global skills directory:

```bash
git clone git@github.com:SeriousMarc/skills.git ~/.claude/skills
```

Then run `/reload-plugins` inside Claude Code to load the skills.

## Updating

```bash
git -C ~/.claude/skills pull
```

Then run `/reload-plugins` inside Claude Code to pick up changes.

## Available Skills

| Skill | Description |
|---|---|
| `python-stack` | Python backend + AI/LLM stack reference for 2026. Covers framework, DB, testing, CI/CD, observability, LLM orchestration, RAG, evals. |

## Usage

All skills have `disable-model-invocation: true` by default — they won't trigger automatically.
Invoke manually when needed:

```
/python-stack
```

To see all available skills in a session:

```
/skills
```

To enable auto-triggering for a skill in a specific project, add to `.claude/settings.json`
in that project:

```json
{
  "skillOverrides": {
    "python-stack": "on"
  }
}
```

## Adding a New Skill

```bash
mkdir ~/.claude/skills/my-skill
```

Create `~/.claude/skills/my-skill/SKILL.md`:

```yaml
---
name: my-skill
description: What this skill does and when to use it.
disable-model-invocation: true
---

# My Skill

Instructions for Claude to follow when this skill is invoked.
```

Commit, push, then run `/reload-plugins` in Claude Code.

## Structure

```
skills/
  python-stack/
    SKILL.md                 # Main skill file, frontmatter + routing
    references/
      backend.md             # Python backend stack reference
      ai-llm.md              # AI/LLM/agentic stack reference
```
