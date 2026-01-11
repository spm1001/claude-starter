# Claude Starter

Set up Claude Code for your team.

## Already have Claude Code installed?

```bash
git clone https://github.com/spm1001/claude-starter ~/Repos/claude-starter
cd ~/Repos/claude-starter
claude
```

Then say "help me set up" or run `/setup`.

---

## First Time? Start Here

Never used Terminal before? Follow these steps exactly.

### How to use these instructions

1. Open this page in your browser
2. For each grey code box below, click it to select, then `Cmd+C` to copy
3. In Terminal, `Cmd+V` to paste, then press `Enter`

### Step 1: Open Terminal

Press `Cmd + Space`, type **Terminal**, press `Enter`.

A window with a command prompt appears. This is where you'll paste commands.

### Step 2: Install Xcode Command Line Tools

```bash
xcode-select --install
```

A popup appears. Click **Install**, then **Agree**.

**Wait 5-10 minutes** for the download to complete.

### Step 3: Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

```

It will ask for your password (the one you use to log into your Mac). Type it and press Enter. You won't see the characters — that's normal.

**Wait 5-10 minutes.** When done, it shows "Next steps".

Run the commands it shows (they look like `echo 'eval...'` and `eval...`). These add Homebrew to your Terminal.

### Step 4: Install required tools

```bash
brew install gh uv node
```

### Step 5: Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

### Step 6: Log into GitHub

```bash
gh auth login
```

When prompted:
- Account: **GitHub.com**
- Protocol: **HTTPS**
- Authenticate: **Yes**
- Method: **Login with a web browser**

Follow the browser prompts to complete login.

### Step 7: Create workspace and get started

```bash
mkdir -p ~/Repos
git clone https://github.com/spm1001/claude-starter ~/Repos/claude-starter
cd ~/Repos/claude-starter
claude
```

Claude Code starts. Say **"help me set up"** and Claude will configure everything.

---

## What's Included

| Tier | What You Get | Source |
|------|--------------|--------|
| **1** | Document skills (docx, pdf, xlsx) + Todoist GTD | This repo |
| **2** | Session lifecycle (`/open`, `/ground`, `/close`) + Beads | claude-advanced |
| **3** | Searchable memory across all sessions | claude-mem |

## Questions?

Ask Sameer or post in #mit-claude-code
