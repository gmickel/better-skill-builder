# Distribution Patterns

## Pattern 1: Git Clone (Simple)

Best for standalone skills:

```bash
git clone https://github.com/user/my-skill ~/.claude/skills/my-skill
```

Example: [raindrop-skill](https://github.com/gmickel/raindrop-skill)

## Pattern 2: CLI Install Command

Best for CLIs with bundled skills:

```bash
mytool skill install --target claude --scope user
mytool skill install --target codex --scope project
```

Implementation: Copy skill files to target directory atomically.

Examples:
- [gno](https://github.com/gmickel/gno): `gno skill install --target claude`
- [sheets-cli](https://github.com/gmickel/sheets-cli): `sheets-cli install-skill --global`

## Pattern 3: Plugin Marketplace

Best for skills bundled with commands/agents:

```bash
/plugin marketplace add https://github.com/user/marketplace-repo
/plugin install my-plugin
```

See [plugin-structure.md](plugin-structure.md) for directory layout.

Example: [flow](https://github.com/gmickel/gmickel-claude-marketplace)

## Pattern 4: CLI --skill Flag

Output skill to stdout for piping:

```bash
mytool --skill > ~/.claude/skills/my-skill/SKILL.md
```

Good for single-file skills. For multi-file, use `skill install`.
