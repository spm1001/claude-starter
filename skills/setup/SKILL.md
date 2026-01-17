---
name: setup
description: >
  Team onboarding installer for Claude Code. Sets up skills, scripts, and hooks
  across three tiers: Tier 1 (document skills + Todoist), Tier 2 (session lifecycle),
  Tier 3 (memory system). Handles repo cloning, symlink creation, and verification.
  Triggers on 'help me set up', 'set up claude', 'install claude tools', '/setup'.
---

# Setup

The installer skill for Claude Code. Configures your environment with skills, scripts, and hooks in three progressive tiers.

## Quick Start

```
/setup              # Interactive — asks which tier
/setup --tier 1     # Just document skills + Todoist
/setup --tier 3     # Full stack (all tiers)
/setup --verify     # Check existing setup
```

## Overview

| Tier | What You Get | Repo |
|------|--------------|------|
| **1** | Document skills (docx, pdf, xlsx) + Todoist GTD | This repo (claude-starter) |
| **2** | Session lifecycle (/open, /close) + Beads | claude-suite |
| **3** | Searchable memory across all sessions | claude-mem |

Each tier builds on the previous. Tier 2 requires Tier 1. Tier 3 requires Tier 2.

## Workflow

### Phase 0: Install Missing Dependencies

Check for and install required tools. Ask user permission before installing anything.

```bash
# Check what's missing
command -v brew &>/dev/null || echo "MISSING: Homebrew"
command -v gh &>/dev/null || echo "MISSING: GitHub CLI"
command -v uv &>/dev/null || echo "MISSING: uv"
```

**If Homebrew is missing:**
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
After install, user needs to run the "Next steps" commands shown (adds brew to PATH).
They may need to restart Terminal or run `eval "$(/opt/homebrew/bin/brew shellenv)"`.

**If GitHub CLI is missing:**
```bash
brew install gh
gh auth login
```
Guide user through: GitHub.com → HTTPS → Yes → Login with browser

**If uv is missing:**
```bash
brew install uv
```

**Create workspace directory:**
```bash
mkdir -p ~/Repos
```

### Phase 1: Gather Current State

Before making changes, check what's already set up:

```bash
# Check if directories exist
ls -la ~/.claude/skills/ 2>/dev/null || echo "No skills directory"
ls -la ~/.claude/scripts/ 2>/dev/null || echo "No scripts directory"
ls -la ~/.claude/hooks/ 2>/dev/null || echo "No hooks directory"

# Check which repos are cloned
ls -d ~/Repos/claude-starter 2>/dev/null && echo "claude-starter: present"
ls -d ~/Repos/claude-advanced 2>/dev/null && echo "claude-advanced: present"
ls -d ~/Repos/claude-mem 2>/dev/null && echo "claude-mem: present"
```

### Phase 2: Ask User Which Tier

Use AskUserQuestion to determine scope:

```
Which setup level do you want?

1. Tier 1 — Document skills + Todoist (basics)
2. Tier 2 — Add session lifecycle (/open, /close) + Beads
3. Tier 3 — Add searchable memory system (full stack)
```

### Phase 3: Execute Setup

Work through each tier sequentially.

---

## Tier 1: Document Skills + Todoist

**Source:** This repo (claude-starter)

### Create Directories

```bash
mkdir -p ~/.claude/skills
mkdir -p ~/.claude/scripts
mkdir -p ~/.claude/hooks
```

### Symlink Skills

From `~/Repos/claude-starter/skills/` to `~/.claude/skills/`:

| Skill | Source Path | Target |
|-------|-------------|--------|
| docx | skills/docx | ~/.claude/skills/docx |
| pdf | skills/pdf | ~/.claude/skills/pdf |
| xlsx | skills/xlsx | ~/.claude/skills/xlsx |
| todoist-gtd | skills/todoist-gtd | ~/.claude/skills/todoist-gtd |
| setup | skills/setup | ~/.claude/skills/setup |

```bash
# Create symlinks (use absolute paths)
STARTER_REPO="$HOME/Repos/claude-starter"

ln -sf "$STARTER_REPO/skills/docx" ~/.claude/skills/docx
ln -sf "$STARTER_REPO/skills/pdf" ~/.claude/skills/pdf
ln -sf "$STARTER_REPO/skills/xlsx" ~/.claude/skills/xlsx
ln -sf "$STARTER_REPO/skills/todoist-gtd" ~/.claude/skills/todoist-gtd
ln -sf "$STARTER_REPO/skills/setup" ~/.claude/skills/setup
```

### Post-Setup: Todoist OAuth

If first time, run OAuth:

```bash
~/.claude/.venv/bin/python ~/Repos/claude-starter/skills/todoist-gtd/scripts/todoist.py auth
```

### Verify Tier 1

```bash
# Check symlinks exist and point to valid targets
ls -la ~/.claude/skills/docx
ls -la ~/.claude/skills/todoist-gtd

# Test Todoist auth
~/.claude/.venv/bin/python ~/Repos/claude-starter/skills/todoist-gtd/scripts/todoist.py auth --status
```

---

## Tier 2: Session Lifecycle

**Source:** claude-advanced repo

### Clone Repo (if needed)

```bash
if [ ! -d ~/Repos/claude-advanced ]; then
    gh repo clone spm1001/claude-advanced ~/Repos/claude-advanced
fi
```

### Symlink Skills

From `~/Repos/claude-suite/skills/` to `~/.claude/skills/`:

| Skill | Source Path | Target |
|-------|-------------|--------|
| session-opening | skills/session-opening | ~/.claude/skills/session-opening |
| session-closing | skills/session-closing | ~/.claude/skills/session-closing |
| beads | skills/beads | ~/.claude/skills/beads |

```bash
SUITE_REPO="$HOME/Repos/claude-suite"

ln -sf "$SUITE_REPO/skills/session-opening" ~/.claude/skills/session-opening
ln -sf "$SUITE_REPO/skills/session-closing" ~/.claude/skills/session-closing
ln -sf "$SUITE_REPO/skills/beads" ~/.claude/skills/beads
```

### Symlink Scripts

From `~/Repos/claude-suite/scripts/` to `~/.claude/scripts/`:

```bash
ln -sf "$SUITE_REPO/scripts/open-context.sh" ~/.claude/scripts/open-context.sh
ln -sf "$SUITE_REPO/scripts/close-context.sh" ~/.claude/scripts/close-context.sh
ln -sf "$SUITE_REPO/scripts/close-extraction.sh" ~/.claude/scripts/close-extraction.sh
ln -sf "$SUITE_REPO/scripts/check-home.sh" ~/.claude/scripts/check-home.sh
```

### Symlink Hooks

```bash
ln -sf "$ADVANCED_REPO/scripts/session-start.sh" ~/.claude/hooks/session-start.sh
```

### Generate Project MCP Config (optional)

If the user will work directly in the claude-advanced directory and needs the workspace MCP:

```bash
# Generate .mcp.json from template, substituting __HOME__ with actual path
sed "s|__HOME__|$HOME|g" "$ADVANCED_REPO/.mcp.json.template" > "$ADVANCED_REPO/.mcp.json"
```

This creates a user-specific `.mcp.json` (gitignored) from the template.

### Post-Setup: Install bd CLI

Beads requires the `bd` CLI:

```bash
# Check if bd is installed
if ! command -v bd &>/dev/null; then
    echo "bd CLI not installed. Install with: cargo install bd"
    echo "Or via Homebrew: brew install bd (if available)"
fi
```

### Verify Tier 2

```bash
# Check skill symlinks
ls -la ~/.claude/skills/session-opening

# Check script symlinks
ls -la ~/.claude/scripts/open-context.sh

# Check hook symlink
ls -la ~/.claude/hooks/session-start.sh

# Test bd
bd --version
```

After verification, tell user to restart Claude (`/exit` then `claude`) to load new skills.

---

## Tier 3: Memory System

**Source:** claude-mem repo

### Clone Repo (if needed)

```bash
if [ ! -d ~/Repos/claude-mem ]; then
    gh repo clone spm1001/claude-mem ~/Repos/claude-mem
fi
```

### Install Dependencies

```bash
cd ~/Repos/claude-mem && uv sync
```

### Create Runtime Directory

```bash
mkdir -p ~/.claude/memory
```

### Symlink Skill

```bash
MEM_REPO="$HOME/Repos/claude-mem"
ln -sf "$MEM_REPO/skill" ~/.claude/skills/mem
```

### Post-Setup: Initial Scan

```bash
cd ~/Repos/claude-mem && uv run mem scan
```

This indexes existing Claude sessions into the memory database.

### Verify Tier 3

```bash
# Check symlink
ls -la ~/.claude/skills/mem

# Check database exists
ls -la ~/.claude/memory/memory.db

# Test mem CLI
cd ~/Repos/claude-mem && uv run mem status
```

---

## Error Handling

### Symlink Already Exists

If a symlink target already exists:

```bash
# Check what it currently points to
ls -la ~/.claude/skills/docx

# If it's a symlink to the wrong place, remove and recreate
rm ~/.claude/skills/docx
ln -sf "$STARTER_REPO/skills/docx" ~/.claude/skills/docx

# If it's a real directory (not symlink), ask user what to do
```

### Repo Clone Fails

If `gh repo clone` fails:
- Check `gh auth status` — user may need to authenticate
- Check network connectivity
- Verify repo exists and user has access

### Permission Issues

If symlink creation fails with permission error:
- Check if ~/.claude/ is writable
- On macOS, check if directory is in a protected location

---

## Verification Checklist

After setup completes, verify:

| Check | Command | Expected |
|-------|---------|----------|
| Skills directory | `ls ~/.claude/skills/` | Lists skill symlinks |
| Tier 1 skills | `ls -la ~/.claude/skills/docx` | Points to claude-starter |
| Tier 2 skills | `ls -la ~/.claude/skills/session-opening` | Points to claude-advanced |
| Tier 3 skill | `ls -la ~/.claude/skills/mem` | Points to claude-mem |
| Scripts | `ls ~/.claude/scripts/` | Lists script symlinks |
| Hooks | `ls ~/.claude/hooks/` | Lists hook symlinks |
| bd CLI | `bd --version` | Shows version |
| mem CLI | `cd ~/Repos/claude-mem && uv run mem status` | Shows database stats |

---

## Updating

To update after initial setup:

```bash
# Pull latest for each repo
cd ~/Repos/claude-starter && git pull
cd ~/Repos/claude-advanced && git pull  # if Tier 2
cd ~/Repos/claude-mem && git pull       # if Tier 3

# Re-sync dependencies (Tier 3)
cd ~/Repos/claude-mem && uv sync
```

Symlinks automatically point to updated content — no need to recreate them.

---

## Uninstalling

To remove a tier:

```bash
# Remove Tier 1 symlinks
rm ~/.claude/skills/{docx,pdf,xlsx,todoist-gtd,setup}

# Remove Tier 2 symlinks
rm ~/.claude/skills/{session-opening,session-closing,beads}
rm ~/.claude/scripts/{open-context.sh,close-context.sh,close-extraction.sh,check-home.sh}
rm ~/.claude/hooks/session-start.sh

# Remove Tier 3 symlinks
rm ~/.claude/skills/mem
```

The source repos can be deleted separately if desired.
