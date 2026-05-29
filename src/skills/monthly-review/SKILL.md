---
name: monthly-review
description: >
  This skill should be used when the user says "monthly review", "end of month",
  "monthly recap", "create monthly note", "monthly goals", "monthly retrospective",
  "how was my month", or "plan next month". Run at the end or start of each month
  to aggregate weekly completions, roll over unfinished tasks, insert monthly
  recurring tasks, and write a structured retrospective note in Obsidian.
metadata:
  version: "0.1.0"
---

## Monthly Review Automation

Run at the end of each month or the start of the next to get a full-month retrospective and plan ahead.

### Step 1 — Locate the vault & monthly notes folder

Identify monthly notes folder:
- `<vault>/Monthly Notes/`
- `<vault>/Journal/Monthly/`

Create it if it doesn't exist.

### Step 2 — Aggregate the month's weekly notes

Read all weekly notes (`Week-{{year}}-W*.md`) whose date range falls within the target month. Collect:
- Total completed tasks across all weeks
- Total incomplete/rolled-over tasks
- Weekly completion rates (to identify best/worst weeks)
- Any text under "Highlights & Learnings" from each weekly note

### Step 3 — Identify open tasks from the month

Also scan any daily notes that aren't captured by weekly notes. Collect all `- [ ]` lines that are still open and whose due date is in the past month.

### Step 4 — Create the monthly note

File name: `{{YYYY-MM}}-{{MonthName}}.md`

```markdown
# {{Month}} {{Year}}

## 🎯 Monthly Goals (set at start of month)
- [ ] 
- [ ] 
- [ ] 

## 📊 Monthly Stats
| Metric | Value |
|--------|-------|
| Total tasks completed | {{completed_total}} |
| Total tasks rolled over | {{incomplete_total}} |
| Overall completion rate | {{completion_rate}}% |
| Best week | W{{best_week}} ({{best_rate}}%) |
| Weakest week | W{{worst_week}} ({{worst_rate}}%) |

## 🔁 Recurring Monthly Tasks
- [ ] Monthly review & retrospective 🔁 every month 📅 {{first_of_month}}
- [ ] Review and update annual goals 🔁 every month 📅 {{first_of_month}}
- [ ] Financial check-in 🔁 every month 📅 {{first_of_month}}
- [ ] Clear and organise vault 🔁 every month 📅 {{last_of_month}}

## 🔄 Rolled Over Tasks
{{incomplete_tasks}}

## 💡 Retrospective

### What went well
> 

### What to improve
> 

### Key learnings
> 

## 🗓️ Next Month's Focus
- [ ] 

## 🔗 Links
- [[Annual Note - {{year}}]]
```

### Step 5 — Report to the user

Summarise:
- Overall completion rate for the month
- Which week was strongest/weakest
- Number of tasks rolled forward
- File path created
