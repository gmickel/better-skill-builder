# gmickel-skill

Guide for building Agent Skills. This repo is itself a skill.

## Structure

```
SKILL.md                      # Main skill (loaded by AI assistants)
README.md                     # GitHub landing page
references/
  patterns.md                 # Detailed patterns
  plugin-structure.md         # Plugin/marketplace format
  real-examples.md            # Production examples
```

## Updating

When updating skill content:
1. Keep SKILL.md under 500 lines (progressive disclosure)
2. Put detailed examples in references/
3. Update real-examples.md when skills change
4. Keep README.md in sync with SKILL.md highlights

## Official Docs

The canonical Agent Skills spec lives at:
- https://agentskills.io/specification
- https://agentskills.io/integrate-skills
- https://agentskills.io/home

If user asks about spec details not covered here, fetch from those URLs.

## Skills Referenced

This repo documents these skills (keep descriptions current):

| Skill | Repo | Pattern |
|-------|------|---------|
| gno | github.com/gmickel/gno | CLI with skill management |
| sheets-cli | github.com/gmickel/sheets-cli | CLI with install-skill |
| raindrop-skill | github.com/gmickel/raindrop-skill | Helper script + git clone |
| outlookctl | github.com/gmickel/outlookctl | Safety-first, nested skill |
| flow | github.com/gmickel/gmickel-claude-marketplace | Plugin bundle |

## Style

- Concise, no fluff
- No em-dashes
- Code examples over prose
- Tables for quick reference
