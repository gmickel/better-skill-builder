---
name: better-skill-builder
description: Guide for building Agent Skills for Claude Code, Codex, Amp, and OpenCode. Use when user asks how to create a skill, build an agent skill, write SKILL.md, distribute skills via plugins, or integrate CLI tools with AI assistants.
---

# Building Agent Skills

Help users build clean, discoverable skills that work across Claude Code, Codex, Amp, and OpenCode.

## Official Spec

Fetch from https://agentskills.io/specification for YAML frontmatter, file format, and client integration details.

## Minimal Structure

```
my-skill/
  SKILL.md           # Required (<500 lines)
  references/        # Optional: detailed docs
  scripts/           # Optional: executable utilities
```

## SKILL.md Essentials

```yaml
---
name: my-skill
description: >
  What it does. Include trigger phrases so AI knows when to activate.
---

# Title

## When to Use
- Trigger condition 1
- Trigger condition 2

## Quick Reference
[Tables, common commands]

## Detailed Docs
See [references/](references/) for full documentation.
```

## References

| Topic | File |
|-------|------|
| Full SKILL.md template | [format.md](references/format.md) |
| Adding scripts | [scripts.md](references/scripts.md) |
| Safety/auth/trigger patterns | [patterns.md](references/patterns.md) |
| Installation paths | [installation.md](references/installation.md) |
| Distribution (git/CLI/plugin) | [distribution.md](references/distribution.md) |
| Plugin/marketplace structure | [plugin-structure.md](references/plugin-structure.md) |
| Production examples | [real-examples.md](references/real-examples.md) |
