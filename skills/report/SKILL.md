---
description: "Report progress of all tasks in the current session/plan. Shows status table of completed, in-progress, and pending work items."
---

# Report Skill

Generate a progress report for the current session by reading the plan file and summarizing task status.

## Instructions

1. **Read the plan file** from the session workspace:
   - Path pattern: `~/.copilot/session-state/*/plan.md`
   - Use the session context to find the exact path

2. **Read recent git history** to determine what has been completed:
   ```bash
   git log --oneline -20
   ```

3. **Cross-reference** the plan tasks against git commits to determine status:
   - ✅ **Done** — a commit exists that addresses this task
   - 🔄 **In Progress** — files have been modified but not committed
   - ⏳ **Pending** — no work started yet
   - ❌ **Failed** — attempted but blocked/failed

4. **Output a formatted table** with these columns:
   | Phase | Task | Status | Commit | Notes |
   |-------|------|--------|--------|-------|

5. **Add a summary footer**:
   - Total tasks, completed, in-progress, pending
   - Any blockers or issues noted

## Output Format

```
## Session Progress Report

### [Plan Title from plan.md]

| Phase | Task | Status | Commit | Notes |
|-------|------|--------|--------|-------|
| 1 | Task description | ✅ Done | abc1234 | — |
| 1 | Task description | 🔄 In Progress | — | Files modified |
| 2 | Task description | ⏳ Pending | — | Blocked by Phase 1 |

### Summary
- **Done:** X / Y tasks
- **In Progress:** X tasks  
- **Pending:** X tasks
- **Blockers:** None / [description]
```
