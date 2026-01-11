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

### How to copy-paste

For each grey code box below:
1. Click the code to select it
2. Press `Cmd+C` to copy
3. In Terminal, press `Cmd+V` to paste
4. Press `Enter` to run it

### Step 1: Open Terminal

Open **Finder** → **Applications** → **Utilities** → double-click **Terminal**.

A window with a command prompt appears.

### Step 2: Install Xcode tools

Type this and press Enter:

```
xcode-select --install
```

A popup appears. Click **Install**, then **Agree**.

**Wait 5-10 minutes** for the download to complete. You'll see "The software was installed" when done.

### Step 3: Install Claude Code

Type this and press Enter:

```
curl -fsSL https://claude.ai/install.sh | bash
```

When it finishes, you'll see a message about adding Claude to your PATH. Copy and run the command it shows (starts with `export PATH=...`).

Then **close Terminal and reopen it** so the PATH takes effect.

### Step 4: Start Claude

Type this and press Enter:

```
claude
```

First time, it asks you to log in. Follow the prompts in your browser.

### Step 5: Set up your tools

Once Claude is running, type this message:

```
help me set up using bit.ly/cc-mit
```

Claude will install any missing tools and configure everything for you.

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
