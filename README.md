# Claude Starter

Set up Claude Code for your team.

## Already have Claude Code?

```bash
git clone https://github.com/spm1001/claude-starter ~/Repos/claude-starter
cd ~/Repos/claude-starter
claude
```

Then say "help me set up" or run `/setup`.

---

## First Time? Start Here

Never used Terminal before? Follow these steps exactly.

### How to copy-paste commands

1. Open this page in your browser
2. For each grey code box, click the code then `Cmd+C` to copy
3. In Terminal, `Cmd+V` to paste, then press `Enter`

### Step 1: Open Terminal

Press `Cmd + Space`, type **Terminal**, press `Enter`.

### Step 2: Install Xcode tools

```bash
xcode-select --install
```

A popup appears. Click **Install**, then **Agree**.

**Wait 5-10 minutes** — this downloads essential developer tools.

### Step 3: Install Claude Code

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### Step 4: Start Claude and set up

```bash
claude
```

First time, it will ask you to log in. Follow the prompts.

Once Claude is running, say:

> **help me set up using bit.ly/cc-mit**

Claude will clone the repo, install any missing tools, and configure everything.

---

## What's Included

| Tier | What You Get | Source |
|------|--------------|--------|
| **1** | Document skills (docx, pdf, xlsx) + Todoist GTD | This repo |
| **2** | Session lifecycle (`/open`, `/ground`, `/close`) + Beads | claude-advanced |
| **3** | Searchable memory across all sessions | claude-mem |

## Questions?

Ask Sameer or post in #mit-claude-code

---

Sources: [Claude Code Setup Docs](https://code.claude.com/docs/en/setup)
