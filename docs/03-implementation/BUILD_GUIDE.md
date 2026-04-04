# Build Guide — Origami Smart Project Management System

**Documentation order:** [README](../../README.md) -> [PRD](../02-product/PRD.md) -> **Build Guide (this file)**

## Purpose

This Build Guide is the canonical implementation document for Origami Smart PM.

Use it to configure the existing product model in Origami without changing the business logic defined in `PRD.md`.

## Build Order

1. Users and Groups
2. User custom fields
3. Project entity
4. Epic entity
5. Task entity
6. Permissions
7. Pages
8. Workflows
9. Gantt
10. QA Team Board
11. Email notifications

Diagram: [`../../assets/diagrams/build-order.drawio`](../../assets/diagrams/build-order.drawio)

## User and Group Setup

Create these groups:
- System Managers
- Project Managers
- Developers / Team Members
- QA Managers
- QA Members
- Viewers

Recommended rule:
- a user may belong to more than one group if needed
- avoid unnecessary overlap in version 1

## Add Custom Fields to Native Users

Add these directly to Users:
- Mobile Number — text
- Department — select / choice
- Job Title — text
- Hourly Rate — numeric range / number selection
- Weekly Capacity Hours — number
- Specialization — text

Constraint:
- in Origami, a custom field cannot point to a Group
- at the project level, use only `user` and `multi-user` fields for ownership and staffing

## Create Project Entity

Add these fields:
- Name
- Description
- Project Goal
- Business Context
- Project Manager
- Delivery Manager
- Delivery Team
- QA Manager
- QA Team
- Status
- Start Date
- End Date
- Budget Planned
- Budget Used
- Progress %

Configure:
- make Goal and Business Context required
- make Budget Used and Progress % workflow-driven
- use built-in metadata in views instead of custom audit fields

## Create Epic Entity

Add these fields:
- Title
- Project
- Description
- Goal
- Owner
- QA Owner
- Status
- Start Date
- End Date
- Progress %

Status values:
- Open
- In Progress
- Ready for QA
- QA
- Done

## Create Task Entity

Add these fields:
- id
- Title
- Description
- Project
- Epic
- Assignee
- QA Assignee
- Status
- Priority
- Due Date
- Start Date
- Estimated Hours
- Actual Hours
- Locked
- Overdue

Task assignment rule:
- `Assignee` is always responsible for making sure the task is actually done
- by default, the same user in `Assignee` also validates the task
- while the Epic is `In Progress`, use `QA Assignee` only when the task needs a second review by QA or by another developer
- in that phase, `QA Assignee` is only a reviewer and does not update the task status
- the reviewer confirms readiness outside the workflow, and the `Assignee` updates the task status
- when the Epic is in `QA`, the QA reviewer may check tasks and return them to `Self QA` if more work is needed
- keep formal routed QA primarily at the Epic level

Task status values:
- New
- InProgress
- Self QA
- Done

Priority values:
- Low
- Medium
- High
- Critical

## Permissions Setup

### System Managers
- full access to all entities and pages

### Project Managers
- full access to Projects, Epics, Tasks
- edit budget and timeline
- see all relevant pages

### Developers / Team Members
- view projects and epics
- edit assigned tasks
- update actual hours
- move task status in allowed flow

### QA Managers
- see QA pages
- edit epics/tasks in QA flow
- receive QA notifications
- assign QA Members

### QA Members
- edit QA-assigned work
- move statuses inside QA flow

### Viewers
- read only

## Page Build Order

1. Projects List
2. Project Details
3. Task Board
4. Epic Board
5. My Tasks
6. QA Queue
7. Dashboard
8. Gantt
9. QA Team Board

## Workflow Build Guide

### WF-01 Task default values
- Trigger: on Task creation
- Actions: `Status = New`, `Locked = false`, `Overdue = false`

### WF-02 Task validation lock
- Trigger: when `Task.Status` changes to `Self QA`
- Action: `Locked = true`
- Restrict editing to `Assignee`, `QA Assignee`, `Project Managers`, `System Managers`

### WF-03 Task unlock
- Trigger: when `Task.Status` changes from `Self QA` to any other value
- Action: `Locked = false`

### WF-04 Overdue flag
- Trigger logic: `Due Date < today` and `Status != Done`
- Action: `Overdue = true`
- Optional: notify `Project Manager`

### WF-05 Project budget rollup
- Trigger: when `Task.Actual Hours` changes
- Action: sum related task hours into `Project.Budget Used`

### WF-06 Epic progress rollup
- Trigger: when `Task.Status` changes
- Action: calculate `Epic.Progress %`
- Suggested formula: `done tasks / total tasks * 100`

### WF-07 Project progress rollup
- Trigger: when `Epic.Progress %` changes
- Action: calculate `Project.Progress %`

### WF-08 Epic QA routing email
- Trigger: when `Epic.Status` changes to `Ready for QA`
- Action: send email to `QA Manager`
- Include Epic, Project, Owner, dates, and direct link if available
- Optional: set `QA Owner` or create QA follow-up action

## Advanced Setup

### Gantt page
- use Project start/end dates
- use Epic start/end dates
- use status color
- use owner display
- group by Project, then show Epic bars underneath
- do not overload version 1 with task-level bars

### QA Team Board
- source: Epics
- statuses: Ready for QA, QA, Done
- use the board for QA Manager triage, QA assignment, and QA visibility

### Email notification setup
- trigger when an Epic enters `Ready for QA`
- recipient = `QA Manager`
- include key project and epic details
