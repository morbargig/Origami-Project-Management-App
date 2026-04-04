# QA Process

## Principle

Execution and validation are intentionally separated into lightweight task-level validation and formal epic-level QA.

## Task-Level Validation

- `Assignee` performs the task work.
- `Assignee` remains responsible for making sure the task is actually done.
- By default, the `Assignee` also validates the task.
- `QA Assignee` is optional.
- `QA Assignee` is only used when a second review is needed.
- While the Epic is `In Progress`, `QA Assignee` is only a reviewer and does not own task status updates.
- The reviewer confirms readiness outside the workflow.
- The `Assignee` updates the task status.

Task status flow:
- `New -> InProgress -> Self QA -> Done`

## Epic-Level QA

- Formal routed QA is primarily handled at the Epic level.
- Epic flow is `Open -> In Progress -> Ready for QA -> QA -> Done`.
- When an Epic becomes `Ready for QA`, `QA Manager` should receive notification or email.
- The QA team handles formal QA routing.
- QA may return work to `In Progress` or send related tasks back to `Self QA` when rework is needed.

## Diagram

QA flow: [`../../assets/diagrams/qa-flow.drawio`](../../assets/diagrams/qa-flow.drawio)
