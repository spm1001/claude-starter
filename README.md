# ITV Claude Code Starter

Get your Claude Code environment configured the team way.

## Quick Start

1. Clone this repo to `~/Repos/`
2. Open Claude in this folder: `cd ~/Repos/claude-starter && claude`
3. Say "help me set up"

Claude will walk you through the rest.

## What's Included

**Tier 1 (this repo):**
- Document skills (docx, xlsx, pdf)
- Todoist GTD skill (MCP-free)
- Google Workspace skill
- myitv search

**Tier 2 (claude-modus):**
- Session lifecycle (`/open`, `/ground`, `/close`)
- Beads multi-session tracking

**Tier 3 (claude-memory):**
- Searchable history across all sessions

## Prerequisites

- Homebrew installed
- GitHub CLI (`gh`) installed and authenticated
- `~/Repos/` folder (local, not cloud-synced)
- Google Drive desktop sync
- Todoist subscription

## Skill Setup

### Todoist GTD

Authenticate with Todoist (one-time):
```bash
~/.claude/.venv/bin/python skills/todoist-gtd/scripts/todoist.py auth
```
Browser opens → click "Authorize" → done.

For SSH sessions, use `--manual` flag.

## Questions?

Ask Sameer or post in #mit-claude-code
