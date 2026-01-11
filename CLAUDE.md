# claude-starter

Team onboarding repo for Claude Code. The "front door" for getting set up.

## First-Time Setup

When a user says "help me set up" or runs `/setup`, use the **setup skill** to configure their environment. The skill handles:

1. **Tier 1** (this repo): Document skills + Todoist GTD
2. **Tier 2** (claude-advanced): Session lifecycle (/open, /ground, /close) + Beads
3. **Tier 3** (claude-mem): Searchable memory across sessions

See `skills/setup/SKILL.md` for detailed instructions.

## What's Here

- Document skills (docx, pdf, xlsx)
- Todoist GTD with OAuth authentication
- The `/setup` installer skill

## Gotchas

### Todoist SDK Bug (Jan 2026)

The `todoist-api-python` SDK's `AuthResult` class expects a `state` field in the token exchange response, but Todoist's API doesn't return it. This causes a parsing error.

**Our workaround:** `todoist_auth.py` bypasses the SDK for token exchange, using direct HTTP to `https://todoist.com/oauth/access_token`. The SDK is fine for everything else.

If the SDK is updated to fix this, our code still works — we just won't benefit from any improvements to their auth handling.

### Client Credentials

`skills/todoist-gtd/scripts/client_credentials.json` contains OAuth client_id and client_secret. This is acceptable because:
- Repo is private
- Client credentials are app identity, not user secrets
- User tokens are stored in Keychain, not the repo

If this repo ever goes public, regenerate the client secret at developer.todoist.com and move credentials to a separate secure location.

## Skills

| Skill | Purpose |
|-------|---------|
| `todoist-gtd` | Todoist integration with GTD coaching, OAuth auth |
| `docx`, `pdf`, `xlsx`, `pptx` | Document creation and manipulation |

## Manual Todoist Auth (if needed)

If /setup doesn't handle Todoist auth automatically:

```bash
~/.claude/.venv/bin/python ~/Repos/claude-starter/skills/todoist-gtd/scripts/todoist.py auth
```

Browser opens → click Authorize → done.
