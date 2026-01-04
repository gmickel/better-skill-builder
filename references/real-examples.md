# Real-World Skill Examples

Production skills demonstrating different patterns.

---

## GNO - Full Skill Management

Local knowledge engine with hybrid search. Most complete skill implementation.

**Pattern:** CLI with built-in skill management commands

**Structure:**
```
gno/
  assets/
    skill/
      SKILL.md           # Main skill
      cli-reference.md   # Full CLI docs
      examples.md        # Usage examples
      mcp-reference.md   # MCP server docs
  src/
    cli/
      commands/
        skill/
          install.ts     # Atomic install via temp + rename
          uninstall.ts
          show.ts        # Preview without installing
          paths.ts       # Show resolved paths
```

**Skill install commands:**
```bash
gno skill install --target claude --scope user
gno skill install --target codex --scope project
gno skill install --target all    # Both
gno skill show                    # Preview files
gno skill paths                   # Show install locations
```

**Key patterns:**
- Multi-target support (claude, codex, all)
- Scope options (user, project)
- Atomic install (temp dir + rename)
- Preview mode before install
- Path debugging command

**SKILL.md excerpt:**
```yaml
---
name: gno
description: >
  Search local documents and knowledge bases. Use when user
  wants to search files, find documents, query notes, look up
  information, index a directory, or needs semantic search.
allowed-tools: Bash(gno:*) Read
---
```

**Repo:** [github.com/gmickel/gno](https://github.com/gmickel/gno)

---

## sheets-cli - CLI with Skill Install

Google Sheets CLI with embedded skill.

**Pattern:** CLI tool with `install-skill` command

**Structure:**
```
sheets-cli/
  SKILL.md              # Skill at repo root
  src/
    cli.ts              # Includes install-skill command
```

**Skill install:**
```bash
sheets-cli install-skill           # Project scope
sheets-cli install-skill --global  # User scope (~/.claude/)
sheets-cli install-skill --codex   # Codex (~/.codex/)
```

**Key patterns:**
- Skill embedded in CLI repo
- Multiple install targets via flags
- Workflow pattern documented (read -> dry-run -> apply)
- Best practices section

**SKILL.md excerpt:**
```yaml
---
name: sheets-cli
description: >
  Read, write, update Google Sheets via CLI. Use when user asks
  to read spreadsheet data, update cells, append rows, or work
  with Google Sheets.
---

## Workflow Pattern

Always: **read -> decide -> dry-run -> apply**
```

**Repo:** [github.com/gmickel/sheets-cli](https://github.com/gmickel/sheets-cli)

---

## raindrop-skill - API Wrapper

Wraps Raindrop.io REST API for bookmark management.

**Pattern:** Helper script + environment variable auth

**Structure:**
```
raindrop-skill/
  SKILL.md
  scripts/
    raindrop.sh         # curl wrapper
  references/
    API-REFERENCE.md    # Full API docs
```

**Install:**
```bash
git clone https://github.com/gmickel/raindrop-skill ~/.claude/skills/raindrop
export RAINDROP_TOKEN="your_token"
```

**Helper script pattern:**
```bash
#!/usr/bin/env bash
set -euo pipefail

BASE_URL="https://api.raindrop.io/rest/v1"

if [[ -z "${RAINDROP_TOKEN:-}" ]]; then
    echo "Error: RAINDROP_TOKEN not set" >&2
    exit 1
fi

METHOD=$(echo "$1" | tr '[:lower:]' '[:upper:]')
ENDPOINT="$2"
BODY="${3:-}"

ARGS=(-s -X "$METHOD" "${BASE_URL}${ENDPOINT}"
      -H "Authorization: Bearer $RAINDROP_TOKEN"
      -H "Content-Type: application/json")

[[ -n "$BODY" ]] && ARGS+=(-d "$BODY")

curl "${ARGS[@]}" | jq .
```

**Key patterns:**
- No CLI needed, just shell script
- Environment variable for auth
- Quick reference tables in SKILL.md
- Full API docs in references/

**Repo:** [github.com/gmickel/raindrop-skill](https://github.com/gmickel/raindrop-skill)

---

## outlookctl - Safety-First Design

Windows Outlook automation via COM.

**Pattern:** Draft-first workflow, explicit confirmation

**Structure:**
```
outlookctl/
  skills/
    outlook-automation/
      SKILL.md
      reference/
        cli.md
        json-schema.md
        security.md
        troubleshooting.md
  src/                  # Python CLI
  tools/
    install_skill.py
```

**Skill install:**
```bash
uv run python tools/install_skill.py --personal
```

**Key patterns:**
- Nested skill directory (skill part of larger CLI)
- Safety rules prominently documented
- Draft-first workflow
- Explicit `--confirm-send YES` required
- Reference docs split by concern

**SKILL.md excerpt:**
```yaml
---
name: outlook-automation
description: >
  Automates Classic Outlook on Windows via COM. Use for email
  and calendar. Requires Classic Outlook running.
---

## Safety Rules

**CRITICAL:**

1. **Never auto-send** - Always create drafts first
2. **Draft-first workflow** - `draft` -> preview -> `send`
3. **Explicit confirmation** - Requires `--confirm-send YES`
```

**Repo:** [github.com/gmickel/outlookctl](https://github.com/gmickel/outlookctl)

---

## Flow - Plugin with Multiple Skills

Plugin bundling 7 skills, 5 commands, 6 agents.

**Pattern:** Plugin marketplace distribution

**Structure:**
```
gmickel-claude-marketplace/
  .claude-plugin/
    marketplace.json
  plugins/
    flow/
      .claude-plugin/
        plugin.json
      skills/
        flow-plan/
          SKILL.md
          steps.md
          examples.md
        flow-work/
          SKILL.md
          phases.md
        interview/
          SKILL.md
        worktree-kit/
          SKILL.md
        rp-explorer/
          SKILL.md
        flow-plan-review/
          SKILL.md
        flow-impl-review/
          SKILL.md
      commands/
        flow/
          plan.md
          work.md
          interview.md
          plan-review.md
          impl-review.md
      agents/
        repo-scout.md
        practice-scout.md
        docs-scout.md
        flow-gap-analyst.md
        quality-auditor.md
        context-scout.md
```

**Install via marketplace:**
```bash
/plugin marketplace add https://github.com/gmickel/gmickel-claude-marketplace
/plugin install flow
```

**Key patterns:**
- Commands invoke skills (stub pattern)
- Skills reference step/phase files
- Agents for parallel research
- Version sync between manifests
- Version bump script

**Command -> Skill pattern:**
```markdown
# commands/flow/plan.md

Invoke the flow-plan skill.
Input: #$ARGUMENTS
```

**Repo:** [github.com/gmickel/gmickel-claude-marketplace](https://github.com/gmickel/gmickel-claude-marketplace)

---

## Pattern Summary

| Skill | Pattern | Auth | Install Method |
|-------|---------|------|----------------|
| gno | Full CLI management | N/A (local) | `gno skill install` |
| sheets-cli | CLI with install cmd | OAuth | `sheets-cli install-skill` |
| raindrop | Helper script | Env var | `git clone` |
| outlookctl | Safety-first | N/A (COM) | Python installer |
| flow | Plugin bundle | N/A | `/plugin install` |
