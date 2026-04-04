# Entities

## Project

### Purpose

The Project is the main management record. It explains the initiative, its goal, time frame, ownership, staffing, and budget.

### Fields

- `Name` - text
- `Description` - long text
- `Project Goal` - long text
- `Business Context` - long text
- `Project Manager` - user
- `Delivery Manager` - user
- `Delivery Team` - multi-user
- `QA Manager` - user
- `QA Team` - multi-user
- `Status` - enum: Draft, Active, On Hold, Completed, Archived
- `Start Date` - date
- `End Date` - date
- `Budget Planned` - number
- `Budget Used` - number, workflow-driven
- `Progress %` - number, workflow-driven

## Epic

### Purpose

An Epic is a major stream of work under a project.

### Fields

- `Title` - text
- `Project` - relation to Project
- `Description` - long text
- `Goal` - long text
- `Owner` - user
- `QA Owner` - user
- `Status` - enum: Open, In Progress, Ready for QA, QA, Done
- `Start Date` - date
- `End Date` - date
- `Progress %` - number, workflow-driven

## Task

### Purpose

The Task is the work unit assigned to a specific person.

### Fields

- `id` - auto-id / readonly
- `Title` - text
- `Description` - long text
- `Project` - relation to Project
- `Epic` - relation to Epic
- `Assignee` - user
- `QA Assignee` - user, optional
- `Status` - enum: New, InProgress, Self QA, Done
- `Priority` - enum: Low, Medium, High, Critical
- `Due Date` - date
- `Start Date` - date
- `Estimated Hours` - number
- `Actual Hours` - number
- `Locked` - boolean
- `Overdue` - boolean, workflow-driven

## Task Responsibility Rule

- `Assignee` is always responsible for making sure the task is actually done.
- By default, the `Assignee` also validates the task.
- `QA Assignee` is optional.
- `QA Assignee` is only used when a second review is needed.
- While the Epic is `In Progress`, `QA Assignee` is only a reviewer and does not own task status updates.
- The reviewer confirms readiness outside the workflow.
- The `Assignee` updates the task status.
- Formal routed QA is primarily handled at the Epic level.

## User Custom Fields

These entity definitions are canonical for the product layer.


Recommended native user fields:
- `Mobile Number`
- `Department`
- `Job Title`
- `Hourly Rate`
- `Weekly Capacity Hours`
- `Specialization`

## Canonical Reference

See [`PRD.md`](PRD.md) for the canonical full entity definitions.
