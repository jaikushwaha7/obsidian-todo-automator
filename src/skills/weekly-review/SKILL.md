---
name: weekly-review
description: >
  This skill should be used when the user says "weekly review", "plan my week",
  "start my week", "weekly check-in", "what did I do this week", "create weekly note",
  "weekly recap", or "weekly rollover". Run this on Monday mornings or Sundays to
  create a weekly note in Obsidian, roll over any unfinished tasks from the past week,
  insert weekly recurring tasks, and produce a progress summary across the 7 days.
metadata:
  version: "0.1.0"
---

## Weekly Review Automation

Run at the start or end of each week to get a structured weekly overview and prepare the coming week.

### Step 1 — Locate the vault & weekly notes folder

If the vault is not yet connected, ask the user to share the folder. Identify the weekly notes folder:
- `<vault>/Weekly Notes/`
- `<vault>/Journal/Weekly/`
- `<vault>/weekly/`

If it doesn't exist, create it.

### Step 2 — Scan the past 7 daily notes

Read each daily note from Mon–Sun (or the past 7 days). For each, collect:
- Completed tasks (`- [x]` lines with `✅`)
- Incomplete tasks (`- [ ]` lines without `✅`)
- Any notes or highlights under `## 🌅 Today's Focus`

Compute totals: completed count, incomplete count, completion rate.

### Step 3 — Create the weekly note

File name: `Week-{{year}}-W{{week_number}}.md`

```markdown
# Week {{week_number}} — {{start_date}} to {{end_date}}

## 🎯 Weekly Goal
> _(What is the one thing that would make this week a success?)_

## 📈 Last Week's Stats
| Metric | Value |
|--------|-------|
| Tasks completed | {{completed_count}} |
| Tasks rolled over | {{incomplete_count}} |
| Completion rate | {{completion_rate}}% |

## 🔁 Recurring Weekly Tasks
- [ ] Weekly review 🔁 every week 📅 {{monday_date}}
- [ ] Clear inbox to zero 🔁 every week 📅 {{monday_date}}
- [ ] Update project trackers 🔁 every week 📅 {{monday_date}}
- [ ] Plan next week's priorities 🔁 every week 📅 {{friday_date}}

## 🔄 Rolled Over from Last Week
{{incomplete_tasks}}

## 📋 This Week's Projects
- [ ] 

## 💡 Highlights & Learnings
> _(What went well? What to improve?)_

## 🔗 Links
- [[Monthly Note - {{month_year}}]]
```

### Step 4 — Update daily notes (optional)

Offer to add a `[[Week {{week_number}}]]` backlink to each daily note from the past week if it doesn't already have one.

### Step 5 — Report to the user

Summarise in chat:
- Completion rate for the past week
- Number of tasks rolled forward
- File path created
- Suggest connecting the monthly review if this is the last week of the month
