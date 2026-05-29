---
name: annual-review
description: >
  This skill should be used when the user says "annual review", "year in review",
  "yearly recap", "create annual note", "set goals for next year", "year-end review",
  "how was my year", or "annual goals". Run once a year (December or January) to
  aggregate monthly stats, review goal completion, roll over unfinished annual tasks,
  and write a structured year-in-review note with next-year planning sections.
metadata:
  version: "0.1.0"
---

## Annual Review Automation

Run at the end of December or start of January to do a full year retrospective and set intentions for the coming year.

### Step 1 — Locate monthly notes for the year

Read all 12 monthly notes (`{{YYYY-MM}}-*.md`) for the target year. If some are missing, note the gaps and work with what's available.

From each monthly note extract:
- Completed task count
- Incomplete/rolled-over count
- Completion rate
- Retrospective highlights (copy "What went well" text)

### Step 2 — Extract annual goals (if set)

Look for an existing annual note from the start of the year. Extract any goals listed under "Annual Goals" or similar heading. Mark each as ✅ achieved or ❌ not achieved based on notes found in monthly reviews.

### Step 3 — Create the annual note

File name: `{{YYYY}}-Annual-Review.md`

```markdown
# {{Year}} Annual Review

## 🏆 Year in Numbers
| Metric | Value |
|--------|-------|
| Total tasks completed | {{yearly_completed}} |
| Total tasks set | {{yearly_total}} |
| Overall completion rate | {{yearly_rate}}% |
| Most productive month | {{best_month}} ({{best_rate}}%) |
| Toughest month | {{worst_month}} ({{worst_rate}}%) |
| Avg weekly completion | {{avg_weekly_rate}}% |

## 📅 Month-by-Month Snapshot
| Month | Completed | Rate |
|-------|-----------|------|
{{monthly_table}}

## 🎯 Goals Review
{{goal_review_table}}

## 🔁 Recurring Annual Tasks
- [ ] Annual review 🔁 every year 📅 {{dec_31}}
- [ ] Set goals for new year 🔁 every year 📅 {{jan_1_next}}
- [ ] Review subscriptions & commitments 🔁 every year 📅 {{jan_1_next}}
- [ ] Update personal README / life document 🔁 every year 📅 {{jan_1_next}}

## 💡 Year Retrospective

### Top 3 wins
1. 
2. 
3. 

### Top 3 lessons
1. 
2. 
3. 

### What to leave behind
> 

### What to carry forward
> 

## 🚀 {{Next Year}} Goals
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 

## 🔗 Monthly Notes
{{monthly_links}}
```

### Step 4 — Report to the user

Summarise:
- Overall yearly completion rate
- Most and least productive month
- How many annual goals were achieved
- File path created
- Offer to generate the open-dashboard for a visual overview
