# 🗂️ Dashboard

> Drop this file into your Obsidian vault root. Requires the **Tasks** and **Dataview** plugins.

---

## 📅 Today

```tasks
not done
due today
sort by priority
```

```tasks
not done
due before today
sort by due
limit 10
```

---

## 🔥 High Priority (Any Date)

```tasks
not done
priority is high
priority is highest
sort by due
```

---

## 📆 This Week

```tasks
not done
due after today
due before in 7 days
sort by due
sort by priority
```

---

## 🔁 Recurring — Due Soon

```tasks
not done
has recurrence
due before in 3 days
sort by due
```

---

## 📊 Stats (last 30 days)

```dataview
TABLE
  length(filter(file.tasks, (t) => t.completed)) AS "✅ Done",
  length(filter(file.tasks, (t) => !t.completed)) AS "⬜ Open",
  round(
    length(filter(file.tasks, (t) => t.completed)) /
    (length(file.tasks) + 0.001) * 100
  ) + "%" AS "Rate"
FROM "Daily Notes"
WHERE file.day >= date(today) - dur(30 days)
SORT file.day DESC
LIMIT 14
```

---

## 📋 Weekly Overview

```dataview
TABLE
  length(filter(file.tasks, (t) => t.completed)) AS "Done",
  length(filter(file.tasks, (t) => !t.completed)) AS "Open"
FROM "Weekly Notes"
SORT file.name DESC
LIMIT 8
```

---

## 🗓️ Monthly Overview

```dataview
TABLE
  length(filter(file.tasks, (t) => t.completed)) AS "Done",
  length(filter(file.tasks, (t) => !t.completed)) AS "Open"
FROM "Monthly Notes"
SORT file.name DESC
LIMIT 6
```

---

## 🔄 Overdue (needs attention)

```tasks
not done
due before today
sort by due
limit 20
```

---

## ✅ Completed Today

```tasks
done
done today
sort by done
```

---

> **Tip:** Pin this file in Obsidian (`Right-click tab → Pin`) and open it on startup.
> Update folder names (`"Daily Notes"`, `"Weekly Notes"`, `"Monthly Notes"`) to match your vault structure.
