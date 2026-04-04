# Workflows

## Workflow Catalog

### WF-01 Task default values
- on task creation
- set `Status = New`
- set `Locked = false`
- set `Overdue = false`

### WF-02 Task validation lock
- when `Task.Status` becomes `Self QA`
- set `Locked = true`
- restrict editing to `Assignee`, `QA Assignee`, `Project Managers`, `System Managers`

### WF-03 Task unlock
- when `Task.Status` changes from `Self QA` to another value
- set `Locked = false`

### WF-04 Overdue flag
- when `Due Date < today`
- and `Status != Done`
- set `Overdue = true`
- optional mail to `Project Manager`

### WF-05 Project budget rollup
- when `Task.Actual Hours` changes
- recalculate `Project.Budget Used`
- version 1 formula: `Budget Used = sum of related Task.Actual Hours`

### WF-06 Epic progress rollup
- when `Task.Status` changes
- update `Epic.Progress %`
- suggested formula: `done tasks / total tasks * 100`

### WF-07 Project progress rollup
- when `Epic.Progress %` changes
- update `Project.Progress %`

### WF-08 Epic QA routing email
- when `Epic.Status` changes to `Ready for QA`
- send email to `QA Manager`
- include Epic, Project, Owner, dates, and link
- optionally set `QA Owner` or create QA follow-up action

## QA Model

### Task Level

- lightweight validation
- default self-validation by `Assignee`
- optional `QA Assignee` reviewer
- task status uses `New -> InProgress -> Self QA -> Done`

### Epic Level

- formal QA flow
- epic status uses `Open -> In Progress -> Ready for QA -> QA -> Done`
- when the Epic becomes `Ready for QA`, `QA Manager` should receive notification or email
- QA team handles formal QA routing

## Canonical Reference

See [`PRD.md`](PRD.md) and [`../03-implementation/BUILD_GUIDE.md`](../03-implementation/BUILD_GUIDE.md) for the canonical workflow baseline.
