# Todoist GTD Skill

Companion skill for the Todoist MCP — adds semantic understanding of GTD structure and outcome quality coaching.

## What This Skill Does

Provides meaning on top of Todoist MCP's data access:
- **3-tier GTD ontology**: Team Priorities → Individual Outcomes → Projects/Actions
- **Outcome quality coaching**: Activity language vs achievement language
- **Pattern detection**: Overcommitment, stale outcomes, missing links
- **Structure awareness**: Outcomes as sections (not tasks)

## Installation

```bash
ln -s /path/to/skill-todoist-gtd ~/.claude/skills/todoist-gtd
```

Requires the Todoist MCP to be configured.

## When Claude Uses This Skill

Activates on:
- "clean up my outcomes", "is this a good outcome?"
- "weekly review", "strategic reflection"
- "check my priorities", "team priorities"

## File Structure

```
todoist-gtd/
├── SKILL.md              # Main skill
└── references/
    ├── TERMINOLOGY.md    # Project/Outcome/Priority disambiguation
    └── COACHING.md       # Outcome quality examples and anti-patterns
```

## Key Concept: Outcomes as Sections

This skill assumes a specific Todoist structure:
- **Outcomes** are SECTIONS in a "Desired Outcomes" project
- **Tasks** live under outcome sections
- Query outcomes with `find_sections()`, not `find_tasks()`

## The 3-Tier Ontology

| Tier | What | Example |
|------|------|---------|
| 1 | Team Priorities | "Expand measurement capabilities" |
| 2 | Individual Outcomes | "Built reporting automation" |
| 3 | Projects & Actions | "Write the script", "Test with data" |

## Outcome Quality

**Activity (bad):** "Write the strategy document"
**Achievement (good):** "Team has clear Q4 direction"

The skill coaches on transforming activity language into achievement language.

## Personalization

This skill encodes one user's GTD structure. Adapt the project names, tier definitions, and Todoist structure to your own setup.

## License

MIT
