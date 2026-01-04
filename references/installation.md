# Installation Paths

## By Client

| Client | User Scope | Project Scope |
|--------|------------|---------------|
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| Codex | `~/.codex/skills/` | `.codex/skills/` |
| Amp | `~/.claude/skills/` | `.claude/skills/` |
| OpenCode | `~/.claude/skills/` | `.claude/skills/` |

## Scope Differences

**User scope** (`~/.claude/skills/`): Available in all projects for that user.

**Project scope** (`.claude/skills/`): Only available in that project. Good for project-specific tooling.

## Name Matching

The `name` field in SKILL.md frontmatter must match the directory name:

```
~/.claude/skills/my-skill/    # Directory name
                 SKILL.md     # name: my-skill (must match)
```
