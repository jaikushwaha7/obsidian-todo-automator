# Obsidian Todo Automator — Claude Cowork Plugin

> Automate your Obsidian task workflow across daily, weekly, monthly, and annual cadences — built as a Claude Cowork plugin using the Claude Agent SDK.

---

## What this is

A Claude Cowork plugin that turns your Obsidian vault into a fully automated productivity system. Instead of manually creating daily notes, copying over unfinished tasks, and tracking your progress week by week — you just say *"daily review"* and Claude does it for you.

It reads your vault, rolls over incomplete tasks, injects recurring tasks for the day, and writes a structured note back — all in the Obsidian Tasks plugin format you already use.

---

## What we built

| Component | What it does |
|-----------|-------------|
| `daily-review` skill | Creates today's daily note, rolls over yesterday's incomplete tasks, injects your 4 top-priority recurring tasks |
| `weekly-review` skill | Aggregates 7 daily notes, computes completion rate, creates weekly note with rollover |
| `monthly-review` skill | Aggregates weekly notes, writes a structured retrospective + next-month planning note |
| `annual-review` skill | Full year stats, goal tracking table, next-year planning section |
| `open-dashboard` skill | Generates a `Dashboard.md` inside your vault using live Tasks + Dataview query blocks |
| Vault permission hook | PreToolUse hook that asks permission before reading or writing your vault or cloud storage |
| Morning scheduled task | Runs `daily-review` automatically at 8 AM every day |

---

## How we built it

This plugin was created entirely through conversation in Claude Cowork using the `create-cowork-plugin` skill. The process:

**1. Requirements gathering** — Claude asked about task management tool (Obsidian), task format (Tasks plugin), desired automations (recurring tasks, rollover, reviews), and dashboard preference. Available connectors were searched live — no Obsidian MCP exists, so the plugin uses direct file system access instead.

**2. Dashboard decision** — Rather than building an external HTML dashboard (which can't check off tasks), we chose an Obsidian-native `Dashboard.md` using live Tasks and Dataview query blocks. This keeps everything inside Obsidian and updates automatically.

**3. Plugin structure** — Five skills, one hooks file, one reference doc. Each skill is a SKILL.md that Claude loads on demand when you say the trigger phrase.

**4. Live test** — Connected the actual vault (`C:\Users\...\Obsidian Vault`), ran `daily-review`, and verified `29-05-2026.md` was created with the correct task structure and custom recurring tasks.

**5. Permission hook** — Added a `PreToolUse` hook that intercepts Read/Write/Edit/Glob/Grep calls and asks for confirmation if the path is inside a vault or cloud storage folder.

**6. Scheduled automation** — Set up a daily 8 AM scheduled task with a self-contained prompt that includes all vault path and formatting preferences.

---

## How to use it

### Prerequisites

- [Claude Cowork](https://claude.ai) desktop app
- Obsidian with the **Tasks plugin** and **Dataview plugin** installed (both free, community plugins)

### Step 1 — Install the plugin

Download `obsidian-todo-automator.plugin` and open it in Claude Cowork. Click **Install** when prompted.

### Step 2 — Drop in the Dashboard

Copy `Dashboard.md` into your Obsidian vault root. Open it in Obsidian and pin the tab — it becomes your home screen, updating live as you tick off tasks.

> Edit the `FROM "Daily Notes"` folder names in the Dataview queries to match your vault's actual folder structure.

### Step 3 — Run your first daily review

In Claude Cowork, say:

> "daily review"

Claude will ask for your vault folder path (one time only), then create today's daily note with your recurring tasks ready to go.

### Step 4 — Customise your recurring tasks

The default top-4 priorities are: Thesis work · Exercise 20 min · German learning · Job search.

To change these, either tell Claude directly ("add meditation to my daily tasks") or edit `skills/daily-review/SKILL.md` inside the installed plugin folder.

### Step 5 — Schedule it

Say: **"schedule daily review every morning at 8am"**

Claude creates a scheduled task that fires automatically each day, rolls over yesterday's incomplete items, and sends you a summary.

### Step 6 — Weekly, monthly, annual

At the end of each week/month/year, say the matching trigger phrase:

| When | Say |
|------|-----|
| Sunday / Monday morning | "weekly review" |
| Last day of month | "monthly review" |
| December / January | "annual review" |

---

## Skill trigger phrases

| Skill | Trigger phrases |
|-------|----------------|
| Daily review | "daily review", "start my day", "what's due today", "morning review" |
| Weekly review | "weekly review", "plan my week", "weekly recap" |
| Monthly review | "monthly review", "end of month", "monthly retro" |
| Annual review | "annual review", "year in review", "yearly recap" |
| Dashboard | "open dashboard", "show my progress", "create dashboard note" |

---

## File structure

```
obsidian-todo-automator/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── daily-review/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── tasks-plugin-format.md   ← full Tasks plugin syntax reference
│   ├── weekly-review/
│   │   └── SKILL.md
│   ├── monthly-review/
│   │   └── SKILL.md
│   ├── annual-review/
│   │   └── SKILL.md
│   └── open-dashboard/
│       └── SKILL.md
├── hooks/
│   └── hooks.json                       ← vault permission gate
└── README.md
```

---

## Customisation

**Change recurring tasks** — Edit the task list in `skills/daily-review/SKILL.md` under "Step 3 — Create today's daily note".

**Change daily note structure** — Edit the template in the same section.

**Change folder names** — Each skill auto-detects folder names, but you can hardcode them in the SKILL.md files if detection ever misses.

**Change permission scope** — Edit `hooks/hooks.json` to add or remove path patterns that trigger the permission prompt.

---

## Adapting for a different task manager

The plugin is Obsidian-specific but the approach works for any local markdown-based system. To adapt:

1. Change the folder paths in each SKILL.md
2. Change the task syntax in `references/tasks-plugin-format.md`
3. If using Notion/Todoist/Asana, connect the relevant MCP and replace the file-read steps with API calls

---

## Built with

- [Claude Cowork](https://claude.ai) — desktop agent with file access
- [Claude Agent SDK](https://docs.claude.ai) — plugin/skill system
- [Obsidian Tasks plugin](https://github.com/obsidian-tasks-group/obsidian-tasks)
- [Obsidian Dataview plugin](https://github.com/blacksmithgu/obsidian-dataview)

---

## Licence

MIT
