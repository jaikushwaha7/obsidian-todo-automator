# Obsidian Tasks Plugin Format Reference

## Basic Task Syntax

```
- [ ] Incomplete task
- [x] Completed task ✅ 2024-01-15
```

## Date Signifiers

| Emoji | Meaning | Example |
|-------|---------|---------|
| 📅 | Due date | `📅 2024-01-15` |
| ⏳ | Scheduled date | `⏳ 2024-01-10` |
| 🛫 | Start date | `🛫 2024-01-08` |
| ✅ | Done date (auto-added) | `✅ 2024-01-15` |
| ❌ | Cancelled date | `❌ 2024-01-15` |

## Priority Signifiers

| Emoji | Priority |
|-------|----------|
| 🔺 | Highest |
| ⏫ | High |
| 🔼 | Medium |
| (none) | Normal |
| 🔽 | Low |
| ⏬ | Lowest |

## Recurrence Signifier

`🔁` followed by a recurrence rule:

```
- [ ] Morning routine 🔁 every day 📅 2024-01-15
- [ ] Weekly review 🔁 every week on Monday 📅 2024-01-15
- [ ] Monthly retro 🔁 every month on the 1st 📅 2024-02-01
- [ ] Annual review 🔁 every year 📅 2024-12-31
```

### Common Recurrence Rules

- `every day`
- `every weekday` (Mon–Fri)
- `every week` / `every week on Monday`
- `every 2 weeks`
- `every month` / `every month on the 1st`
- `every 3 months`
- `every year`

## Tags and IDs

Tasks can have tags: `#area/work`, `#project/launch`

Task IDs (for blocking/blocked-by relationships):
```
- [ ] Task A 🆔 abc123
- [ ] Task B ⛔ abc123
```

## Completion Behaviour

When a recurring task is completed, the Tasks plugin automatically creates the NEXT occurrence. When writing recurring tasks manually (outside the plugin UI), create them with the **next** due date — the plugin handles future instances.

## Querying Tasks (Dataview / Tasks plugin blocks)

```tasks
not done
due today
sort by priority
```

```tasks
done
done after 2024-01-01
group by done
```

## File Naming Conventions (Daily Notes)

Common formats:
- `YYYY-MM-DD.md` → `2024-01-15.md`
- `DD-MM-YYYY.md` → `15-01-2024.md`
- `MMMM D, YYYY.md` → `January 15, 2024.md`

Weekly:
- `GGGG-[W]WW.md` → `2024-W03.md`
- `Week-YYYY-WW.md` → `Week-2024-03.md`

Monthly:
- `YYYY-MM.md` → `2024-01.md`
- `YYYY-MM MMMM.md` → `2024-01 January.md`
