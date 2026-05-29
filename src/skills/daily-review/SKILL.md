---
name: daily-review
description: >
  This skill should be used when the user says "daily review", "start my day",
  "morning review", "what's due today", "create today's tasks", "daily check-in",
  or "roll over yesterday's tasks". Use it to run the daily automation cycle on
  their Obsidian vault: create today's daily note with recurring tasks, identify
  unfinished items from yesterday, roll them forward, and produce a focused summary
  of what's on the agenda for the day.
metadata:
  version: "0.1.0"
---

## Daily Review Automation

Run this skill at the start of each day to prepare the day's task list in Obsidian.

### Step 1 — Locate the vault

Ask the user to select their Obsidian vault folder (using `mcp__cowork__request_cowork_directory`) if not already connected. The vault root is the folder containing the `.obsidian/` directory.

Identify the daily notes folder. Common locations:
- `<vault>/Daily Notes/`
- `<vault>/Journal/`
- `<vault>/daily/`

If unclear, ask the user where their daily notes live.

### Step 2 — Check yesterday's note

Find yesterday's daily note file (format: `YYYY-MM-DD.md` or locale variant the user uses). Read it and extract all incomplete tasks:

```
- [ ] task text 📅 YYYY-MM-DD
- [ ] task text ⏫ 🔁 every day
```

Collect every line matching `- [ ]` that does not have `✅` on it.

See `references/tasks-plugin-format.md` for full syntax reference.

### Step 3 — Create today's daily note

Create `<daily-notes-folder>/YYYY-MM-DD.md` (today's date). If the file already exists, append to it rather than overwriting.

Structure the note:

```markdown
# Daily Note — {{date:MMMM D, YYYY}}

## 🌅 Today's Focus
> _(Write one sentence about what matters most today)_

## ✅ Tasks

### 🔁 Recurring
- [ ] Morning routine 🔁 every day 📅 {{date}}
- [ ] Review inbox 🔁 every day 📅 {{date}}
- [ ] End-of-day shutdown 🔁 every day 📅 {{date}}

### 🔄 Rolled Over from Yesterday
{{rolled_over_tasks}}

### ➕ New Today
- [ ] 

## 📊 Progress Check
- Completed yesterday: {{completed_count}}
- Rolled over: {{rolled_count}}
- Mood: 

## 🔗 Links
- [[Weekly Note - W{{week_number}}]]
```

Replace `{{rolled_over_tasks}}` with the incomplete tasks collected in Step 2, updating their 📅 date to today.

### Step 4 — Report to the user

After writing the file, summarise in chat:
- How many tasks were rolled over
- How many recurring tasks were added
- The file path created
- Offer to open the dashboard (`open-dashboard` skill)

Do not dump the entire file contents in chat — keep the summary brief (3–5 lines).
