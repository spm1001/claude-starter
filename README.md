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

---

### Step 1: Open Terminal

Open **Finder** → **Applications** → **Utilities** → double-click **Terminal**.

You'll see a window like this:

```
┌─────────────────────────────────────────────────────────────────┐
│ Terminal                                                         │
├─────────────────────────────────────────────────────────────────┤
│ Last login: Fri Jan 10 14:32:01 on ttys000                      │
│ yourname@Mac ~ %                                                 │
│                                                                  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

The `%` is where you type commands.

---

### Step 2: Install Xcode tools

Type this and press Enter:

```
xcode-select --install
```

A popup appears:

```
┌────────────────────────────────────────────┐
│                                            │
│  "xcode-select" requires command line      │
│  developer tools. Would you like to        │
│  install them now?                         │
│                                            │
│         [ Cancel ]  [ Install ]            │
│                                            │
└────────────────────────────────────────────┘
```

Click **Install**, then **Agree** to the license.

**Wait 5-10 minutes.** When done, you'll see "The software was installed."

*If the popup doesn't appear, Xcode tools are already installed. Continue to Step 3.*

---

### Step 3: Install Claude Code

Type this and press Enter:

```
curl -fsSL https://claude.ai/install.sh | bash
```

You'll see installation progress, then something like:

```
┌─────────────────────────────────────────────────────────────────┐
│ Terminal                                                         │
├─────────────────────────────────────────────────────────────────┤
│ Downloading Claude Code...                                       │
│ Installing to ~/.claude/bin/claude                               │
│ Done!                                                            │
│                                                                  │
│ To use Claude, add it to your PATH by running:                   │
│                                                                  │
│   export PATH="$HOME/.claude/bin:$PATH"                          │
│                                                                  │
│ yourname@Mac ~ %                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Copy that `export PATH=...` line and paste it, then press Enter.**

Then **quit Terminal** (Cmd+Q) and **open it again** so the change takes effect.

---

### Step 4: Download the starter kit

Type this and press Enter:

```
mkdir -p ~/Repos && git clone https://github.com/spm1001/claude-starter ~/Repos/claude-starter && cd ~/Repos/claude-starter
```

You'll see:

```
┌─────────────────────────────────────────────────────────────────┐
│ Terminal                                                         │
├─────────────────────────────────────────────────────────────────┤
│ Cloning into '/Users/yourname/Repos/claude-starter'...          │
│ remote: Enumerating objects: 142, done.                         │
│ remote: Counting objects: 100% (142/142), done.                 │
│ Receiving objects: 100% (142/142), 1.24 MiB | 5.2 MiB/s, done.  │
│ yourname@Mac claude-starter %                                    │
└─────────────────────────────────────────────────────────────────┘
```

Notice the prompt now shows `claude-starter` — you're in the right folder.

---

### Step 5: Start Claude

Type this and press Enter:

```
claude
```

First time, Claude asks you to log in:

```
┌─────────────────────────────────────────────────────────────────┐
│ Terminal                                                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Welcome to Claude Code!                                         │
│                                                                  │
│  Press Enter to open the browser and log in...                   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

Press Enter, log in via your browser, then return to Terminal.

---

### Step 6: Set up your tools

**You're now chatting with Claude** — not running commands.

Type this message and press Enter:

```
help me set up
```

```
┌─────────────────────────────────────────────────────────────────┐
│ Claude Code                                                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  > help me set up                                                │
│                                                                  │
│  I'll help you set up your Claude Code environment. Let me      │
│  check what tier you'd like to install...                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

Claude will install any missing tools (Homebrew, GitHub CLI, etc.) and configure everything.

---

## What's Included

| Tier | What You Get | Source |
|------|--------------|--------|
| **1** | Document skills (docx, pdf, xlsx) + Todoist GTD | This repo |
| **2** | Session lifecycle (`/open`, `/ground`, `/close`) + Beads | claude-advanced |
| **3** | Searchable memory across all sessions | claude-mem |

## Troubleshooting

**"command not found: claude"**
The PATH wasn't set. Go back to Step 3 and run the `export PATH=...` command, then quit and reopen Terminal.

**"command not found: git"**
Xcode tools didn't install. Go back to Step 2.

**The popup in Step 2 didn't appear**
Xcode tools are probably already installed. Continue to Step 3.

## Questions?

Ask Sameer or post in #mit-claude-code

---

Sources: [Claude Code Setup Docs](https://code.claude.com/docs/en/setup)
