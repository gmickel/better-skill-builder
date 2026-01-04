# SKILL.md Format Template

Full template with all common sections:

```yaml
---
name: my-skill
description: >
  What this skill does and when to use it.
  Include trigger phrases the AI should recognize.
allowed-tools: Bash(mytool:*) Read  # Optional: restrict tools
---

# Skill Title

Brief intro paragraph.

## When to Use This Skill

- Trigger condition 1
- Trigger condition 2

## Quick Reference

| Command | Description |
|---------|-------------|
| `cmd one` | Does X |
| `cmd two` | Does Y |

## Common Workflows

### Workflow Name
```bash
# Step 1
mytool do-thing

# Step 2
mytool other-thing
```

## Reference Documentation

For detailed info, see:
- [cli-reference.md](references/cli-reference.md)
- [examples.md](references/examples.md)
```

## Frontmatter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Must match directory name |
| `description` | Yes | Include trigger phrases |
| `allowed-tools` | No | Restrict available tools |
