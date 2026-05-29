---
name: open-dashboard
description: >
  This skill should be used when the user says "open dashboard", "show dashboard",
  "task dashboard", "show my progress", "todo overview", "productivity dashboard",
  "update dashboard", "create dashboard note", or "dashboard in obsidian". Creates or
  regenerates a Dashboard.md file inside the user's Obsidian vault using live Tasks
  plugin query blocks and Dataview tables — so it always shows current data without
  leaving Obsidian.
metadata:
  version: "0.1.0"
---

## Obsidian-Native Dashboard

Create or update `Dashboard.md` in the vault root. This file uses live Tasks and Dataview query blocks — no external tool needed.

### Step 1 — Confirm vault access

Ensure the vault folder is connected. If not, request it via `mcp__cowork__request_cowork_directory`.

### Step 2 — Detect folder names

Scan the vault root to find the actual names of the daily/weekly/monthly notes folders. Common variants:
- Daily: `Daily Notes`, `Journal`, `daily`, `Days`
- Weekly: `Weekly Notes`, `Journal/Weekly`, `weekly`
- Monthly: `Monthly Notes`, `Journal/Monthly`, `monthly`

Use the detected names in the Dataview queries — do not hardcode defaults.

### Step 3 — Write Dashboard.md

Create `<vault-root>/Dashboard.md` with the following structure. Substitute detected folder names into the Dataview `FROM` clauses.

```markdown
# 🗂️ Dashboard

> Auto-updates as you complete tasks. Pin this tab in Obsidian for quick access.

---

## 📅 Today

​```tasks
not done
due today
sort by priority
​```

​```tasks
not done
due before today
sort by due
limit 10
​```

---

## 🔥 High Priority

​```tasks
not done
priority is high
priority is highest
sort by due
​```

---

## 📆 This Week

​```tasks
not done
due after today
due before in 7 days
sort by due
sort by priority
​```

---

## 🔁 Recurring — Due Soon

​```tasks
not done
has recurrence
due before in 3 days
sort by due
​```

---

## 📊 Daily Stats (last 14 days)

​```dataview
TABLE
  length(filter(file.tasks, (t) => t.completed)) AS "✅ Done",
  length(filter(file.tasks, (t) => !t.completed)) AS "⬜ Open",
  round(length(filter(file.tasks, (t) => t.completed)) / (length(file.tasks) + 0.001) * 100) + "%" AS "Rate"
FROM "<daily-folder>"
WHERE file.day >= date(today) - dur(14 days)
SORT file.day DESC
​```

---

## 📋 Weekly Summary

​```dataview
TABLE
  length(filter(file.tasks, (t) => t.completed)) AS "Done",
  length(filter(file.tasks, (t) => !t.completed)) AS "Open"
FROM "<weekly-folder>"
SORT file.name DESC
LIMIT 8
​```

---

## 🗓️ Monthly Summary

​```dataview
TABLE
  length(filter(file.tasks, (t) => t.completed)) AS "Done",
  length(filter(file.tasks, (t) => !t.completed)) AS "Open"
FROM "<monthly-folder>"
SORT file.name DESC
LIMIT 6
​```

---

## 🔄 Overdue

​```tasks
not done
due before today
sort by due
limit 20
​```

---

## ✅ Completed Today

​```tasks
done
done today
​```
```

### Step 4 — Tell the user

After writing the file:
- Confirm the vault path where `Dashboard.md` was created
- Tell them to open it in Obsidian and pin the tab (`Right-click tab → Pin`) so it's always visible on startup
- Remind them the Dataview and Tasks plugins must be installed for the queries to render
- Note that folder names were auto-detected (or ask them to confirm if uncertain)
