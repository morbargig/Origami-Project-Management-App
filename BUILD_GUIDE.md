# Build Guide — Origami Smart Project Management System

**Documentation order:** [README](README.md) → [PRD](PRD.md) → **Build Guide (this file)**

<a id="build-main-doc"></a>

<a id="toc-build"></a>

## Table of Contents

### In this document
- **[[V1 Core] 1. Build Order](#build-1)**
- **[[V1 Core] 2. User and Group Setup](#build-2)**
- **[[V1 Core] 3. Add Custom Fields to Native Users](#build-3)**
- **[[V1 Core] 4. Create Project Entity](#build-4)**
- **[[V1 Core] 5. Create Epic Entity](#build-5)**
- **[[V1 Core] 6. Create Task Entity](#build-6)**
- **[[V1 Core] 7. Permissions Setup](#build-7)**
- **[[V1 Core] 8. Page Build Order](#build-8)**
- **[[V1 Core] 9. Workflow Build Guide](#build-9)**
- **[[V2 Advanced] 10. Gantt Page Setup](#build-10)**
- **[[V2 Advanced] 11. QA Team Board Setup](#build-11)**
- **[[V2 Advanced] 12. Email Notification Setup](#build-12)**

---

<a id="build-1"></a>

## [V1 Core] 1. Build Order

Build in this order:

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

This order keeps the model stable before UI and automation.

---

<a id="build-2"></a>

## [V1 Core] 2. User and Group Setup

Create these groups:
- System Managers
- Project Managers
- Developers / Team Members
- QA Managers
- QA Members
- Viewers

Then assign users into groups according to responsibility.

### Recommended rule
A user may belong to more than one group if needed, but avoid unnecessary overlap in version 1.

---

<a id="build-3"></a>

## [V1 Core] 3. Add Custom Fields to Native Users

Since your Origami environment supports custom user fields, add these directly to Users:

- Department — text or enum
- Job Title — text
- Hourly Rate — number
- Weekly Capacity Hours — number
- Primary Team — enum or relation
- QA Specialization — text or enum

The most useful first ones are:
- Primary Team
- Hourly Rate
- Weekly Capacity Hours

---

<a id="build-4"></a>

## [V1 Core] 4. Create Project Entity

Add these fields:

- Name — text
- Description — long text
- Project Goal — long text
- Business Context — long text
- Project Manager — user
- Delivery Team — enum/relation
- QA Team — enum/relation
- QA Manager — user
- Status — enum
- Start Date — date
- End Date — date
- Budget Planned — number
- Budget Used — number
- Progress % — number

### Configure
- make Goal and Business Context required
- make Budget Used and Progress % workflow-driven
- use built-in metadata in views instead of custom audit fields

---

<a id="build-5"></a>

## [V1 Core] 5. Create Epic Entity

Add these fields:

- Title — text
- Project — relation to Project
- Description — long text
- Goal — long text
- Owner — user
- QA Owner — user
- Status — enum
- Start Date — date
- End Date — date
- Progress % — number

### Status values
- Open
- In Progress
- Ready for QA
- QA
- Done

---

<a id="build-6"></a>

## [V1 Core] 6. Create Task Entity

Add these fields:

- Title — text
- Description — long text
- Project — relation to Project
- Epic — relation to Epic
- Assignee — user
- Task QA Owner — user
- Status — enum
- Priority — enum
- Start Date — date
- Due Date — date
- Estimated Hours — number
- Actual Hours — number
- Locked — boolean
- Overdue — boolean

### Status values
- New
- In Progress
- Ready for QA
- QA
- Done

### Priority values
- Low
- Medium
- High
- Critical

---

<a id="build-7"></a>

## [V1 Core] 7. Permissions Setup

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

---

<a id="build-8"></a>

## [V1 Core] 8. Page Build Order

Build pages in this order:

1. Projects List
2. Project Details
3. Task Board
4. Epic Board
5. My Tasks
6. QA Queue
7. Dashboard
8. Gantt
9. QA Team Board

### Why this order
It gives usable operations early, then management views, then advanced timeline pages.

---

<a id="build-9"></a>

## [V1 Core] 9. Workflow Build Guide

## WF-01 Task default values

### Trigger
- on Task creation

### Actions
- Status = New
- Locked = false
- Overdue = false

---

## WF-02 Task QA lock

### Trigger
- when Task.Status changes to QA

### Actions
- Locked = true

### Permission effect
- restrict editing to QA Members, QA Managers, Project Managers, System Managers

---

## WF-03 Task unlock

### Trigger
- when Task.Status changes from QA to any other value

### Actions
- Locked = false

---

## WF-04 Overdue flag

### Trigger logic
- Due Date < today
- AND Status != Done

### Actions
- Overdue = true
- optional email to Project Manager

### How to implement
1. Create a workflow triggered on task update or scheduled condition
2. Add condition: due date earlier than current date
3. Add condition: status is not Done
4. Add action: set Overdue = true
5. Optionally add action: send email / notification

---

## WF-05 Project budget rollup

### Trigger
- when Task.Actual Hours changes

### Actions
- sum all Actual Hours of tasks related to the same Project
- set Project.Budget Used

---

## WF-06 Epic progress rollup

### Trigger
- when Task.Status changes

### Actions
- calculate Epic.Progress % from related tasks

### Suggested formula

```text
done tasks / total tasks * 100
```

---

## WF-07 Project progress rollup

### Trigger
- when Epic.Progress % changes

### Actions
- calculate Project.Progress %

---

## WF-08 Epic QA routing email

### Trigger
- when Epic.Status changes to Ready for QA

### Actions
- send email to QA Manager
- include Epic, Project, Owner, dates, and a direct link if available
- optionally set QA Owner or create a follow-up QA action

---

<a id="build-10"></a>

## [V2 Advanced] 10. Gantt Page Setup

Create a Gantt/timeline page using:

- Project start/end dates
- Epic start/end dates
- status color
- owner display

### Recommended first view
Group by Project, then show Epic bars underneath.

Do not overload it with task-level bars in version 1.

---

<a id="build-11"></a>

## [V2 Advanced] 11. QA Team Board Setup

Create a separate Kanban page for QA.

### Source
- Epics

### Statuses
- Ready for QA
- QA
- Done

Use this page for:
- QA Manager triage
- QA assignment
- QA team visibility

---

<a id="build-12"></a>

## [V2 Advanced] 12. Email Notification Setup

For Epic QA routing:
- trigger when Epic enters Ready for QA
- recipient = QA Manager
- include key project and epic details

Optional later:
- notify assigned QA Member
- notify Project Manager when QA is completed
- notify Developer when Epic is returned from QA

---

### Other documents
- [← README — how to use this documentation](README.md)
- [← PRD — product requirements](PRD.md)
