# PRD — Origami Smart Project Management System

**Documentation order:** [README](README.md) → **PRD (this file)** → [Build Guide](BUILD_GUIDE.md)

<a id="prd-main-doc"></a>

<a id="toc-prd"></a>

## Table of Contents

### In this document
- **[[V1 Core] 1. Executive Summary](#prd-1)**
- **[[V1 Core] 2. Project Management Background and Mindset](#prd-2)**
- **[[V1 Core] 3. Product Vision](#prd-3)**
- **[[V1 Core] 4. Target Users](#prd-4)**
- **[[V1 Core] 5. System Scope](#prd-5)**
- **[[V1 Core] 6. Core Structure: Project → Epic → Task](#prd-6)**
- **[[V1 Core] 7. Teams, Ownership, and QA Structure](#prd-7)**
- **[[V1 Core] 8. Native Origami Capabilities Used](#prd-8)**
- **[[V1 Core] 9. Entity Catalog](#prd-9)**
- **[[V1 Core] 10. Page Catalog and Visual Experience](#prd-10)**
- **[[V1 Core] 11. Workflow Catalog](#prd-11)**
- **[[V1 Core] 12. Notifications and QA Flow](#prd-12)**
- **[[V1 Core] 13. Budget and Timeline Logic](#prd-13)**
- **[[V2 Advanced] 14. Gantt / Timeline Experience](#prd-14)**
- **[[V2 Advanced] 15. QA Team Board](#prd-15)**
- **[[V2 Advanced] 16. Reporting and Dashboards](#prd-16)**
- **[[V3 Optional] 17. Future Enhancements](#prd-17)**

### Other documents
- [← README — how to use this documentation](README.md)
- [Build Guide — Origami implementation →](BUILD_GUIDE.md)

---

<a id="prd-1"></a>

## [V1 Core] 1. Executive Summary

This project is a **smart project management system built on Origami** for medium-size teams.

Its purpose is to help managers define project goals clearly, break work into structured levels, manage execution, track time and budget simply, and control delivery through permissions, workflows, and visual pages.

This system is not only a task board. It is a **project management operating model** based on:

- context
- time
- resources
- budget
- quality gates
- manager visibility

Project management commonly balances scope, time, and cost, while maintaining quality. That mindset is reflected directly in this app design.

---

<a id="prd-2"></a>

## [V1 Core] 2. Project Management Background and Mindset

A project manager is not just someone who assigns tasks. A project manager is responsible for turning an idea into a controlled delivery outcome.

This app is built around a simple learning and operating mindset:

```text
Context → Goal → Plan → Execution → Control → Delivery
```

And inside the system:

```text
Project → Epic → Task → QA → Timeline → Budget → Dashboard
```

Each system part maps directly to a project-management concept:

- **Business Context** = why the project exists
- **Project Goal** = what success looks like
- **Dates / Gantt** = time planning
- **Users / Teams / QA** = resources and responsibility
- **Budget fields** = cost control
- **QA flow** = quality control
- **Dashboards** = governance and visibility

This makes the app useful both as a real operational system and as a teaching structure for project-manager students.

---

<a id="prd-3"></a>

## [V1 Core] 3. Product Vision

The vision is to create a single Origami workspace where a manager can:

- define a project clearly
- connect the project to a responsible team
- divide the project into epics
- divide epics into tasks
- send work through controlled QA stages
- monitor timeline visually
- track budget simply
- give each team the right page and permissions

---

<a id="prd-4"></a>

## [V1 Core] 4. Target Users

This system is designed for four main audiences.

### Project Managers
Need full project visibility, timeline control, budget awareness, and QA escalation.

### Team Members / Developers
Need clear task ownership, due dates, status flow, and a focused “My Work” view.

### QA Team
Need separate visibility for items ready for validation, assignment to QA members, and status progression through QA.

### Stakeholders / Clients / Managers
Need dashboards, progress indicators, and project-level summaries without operational clutter.

---

<a id="prd-5"></a>

## [V1 Core] 5. System Scope

The first production scope includes:

- Projects
- Epics
- Tasks
- Native Origami Users
- Native Origami Groups
- Native metadata fields
- Gantt / timeline page
- Task Kanban
- Epic Kanban
- QA Kanban
- Dashboard
- Budget tracking
- Notifications
- Workflows

The first version does **not** need deep financial ERP logic, billing complexity, or advanced dependency engines.

---

<a id="prd-6"></a>

## [V1 Core] 6. Core Structure: Project → Epic → Task

This is the heart of the system:

```text
Project
   ├── Epic
   │     ├── Task
   │     ├── Task
   │
   ├── Epic
         ├── Task
         ├── Task
```

- **Project** = manager level
- **Epic** = workstream or major deliverable
- **Task** = execution level

This structure keeps the system readable for managers and teachable for students.

---

<a id="prd-7"></a>

## [V1 Core] 7. Teams, Ownership, and QA Structure

This system should use **Origami native Users and Groups**.

Important Origami constraint: custom fields cannot point to a Group. At the project level, use only `user` and `multi-user` fields for ownership and staffing.

### Recommended groups
- **System Managers**
- **Project Managers**
- **Developers / Team Members**
- **QA Managers**
- **QA Members**
- **Viewers**

Using **System Manager** instead of “Admin” is a good naming choice if that matches your internal language.

### How projects connect to teams

Each Project should have:

- a **Project Manager**
- a **Delivery Manager**
- a **Delivery Team**
- a **QA Manager**
- a **QA Team**

Recommended fields on Project:

- `Project Manager` — user
- `Delivery Manager` — user
- `Delivery Team` — multi-user
- `QA Manager` — user
- `QA Team` — multi-user

This gives flexibility for:

- clear accountable owners per delivery and QA stream
- visible staffing using user-based fields only
- reporting by manager and by assigned team members

### One QA team or several?

Use **one QA team** when:

- the organization is small or medium
- QA handles all projects centrally
- you want simpler routing

Use **multiple QA teams** when:

- projects belong to different business domains
- teams test different systems or specialties
- each project family has different QA ownership

For a medium-size first version, one central QA team plus a QA manager is usually the cleanest start.

---

<a id="prd-8"></a>

## [V1 Core] 8. Native Origami Capabilities Used

This project intentionally uses Origami natively for:

- Users
- Groups
- System metadata such as created at, created by, updated at, updated by, id
- Custom fields
- Workflows
- Dashboards
- Gantt / Kanban / table views
- Permissions

Since your Origami environment supports custom user fields, user attributes like **Hourly Rate**, **Department**, **Capacity**, or **Team Role** can be stored directly on the User object.

---

<a id="prd-9"></a>

## [V1 Core] 9. Entity Catalog

## Project

### Purpose
The Project is the main management record. It explains the initiative, its goal, time frame, ownership, staffing, and budget.

### Fields

#### Name
- **Type:** text
- **Required:** yes
- **Purpose:** project title

#### Description
- **Type:** long text
- **Required:** yes
- **Purpose:** summary of the project

#### Project Goal
- **Type:** long text
- **Required:** yes
- **Purpose:** the expected business or delivery outcome

#### Business Context
- **Type:** long text
- **Required:** yes
- **Purpose:** why this project exists and what need it solves

#### Project Manager
- **Type:** user
- **Required:** yes
- **Purpose:** single accountable owner

#### Delivery Manager
- **Type:** user
- **Required:** yes
- **Purpose:** day-to-day delivery lead for the project

#### Delivery Team
- **Type:** multi-user
- **Required:** yes
- **Purpose:** the delivery users assigned to the project

#### QA Manager
- **Type:** user
- **Required:** yes
- **Purpose:** escalation and QA routing owner

#### QA Team
- **Type:** multi-user
- **Required:** yes
- **Purpose:** the QA users assigned to the project

#### Status
- **Type:** enum
- **Values:** Draft, Active, On Hold, Completed, Archived
- **Required:** yes

#### Start Date
- **Type:** date
- **Required:** yes

#### End Date
- **Type:** date
- **Required:** yes

#### Budget Planned
- **Type:** number
- **Required:** yes
- **Purpose:** approved project budget

#### Budget Used
- **Type:** number
- **Calculated/workflow-driven:** yes
- **Purpose:** current consumed budget

#### Progress %
- **Type:** number
- **Calculated/workflow-driven:** yes
- **Purpose:** project progress from child work

---

## Epic

### Purpose
An Epic is a major stream of work under a project.

### Fields

#### Title
- **Type:** text
- **Required:** yes

#### Project
- **Type:** relation to Project
- **Required:** yes

#### Description
- **Type:** long text
- **Required:** yes

#### Goal
- **Type:** long text
- **Required:** no, recommended

#### Owner
- **Type:** user
- **Required:** yes

#### QA Owner
- **Type:** user
- **Required:** no
- **Purpose:** epic-level QA lead if needed

#### Status
- **Type:** enum
- **Values:** Open, In Progress, Ready for QA, QA, Done
- **Required:** yes

#### Start Date
- **Type:** date
- **Required:** yes

#### End Date
- **Type:** date
- **Required:** yes

#### Progress %
- **Type:** number
- **Calculated/workflow-driven:** yes

---

## Task

### Purpose
The Task is the work unit assigned to a specific person.

### Fields

#### Title
- **Type:** text
- **Required:** yes

#### Description
- **Type:** long text
- **Required:** no

#### Project
- **Type:** relation to Project
- **Required:** yes

#### Epic
- **Type:** relation to Epic
- **Required:** yes

#### Assignee
- **Type:** user
- **Required:** yes

#### Task QA Owner
- **Type:** user
- **Required:** no
- **Purpose:** the QA person responsible for the task if needed

#### Status
- **Type:** enum
- **Values:** New, In Progress, Ready for QA, QA, Done
- **Required:** yes

#### Priority
- **Type:** enum
- **Values:** Low, Medium, High, Critical
- **Required:** yes

#### Start Date
- **Type:** date
- **Required:** no

#### Due Date
- **Type:** date
- **Required:** yes

#### Estimated Hours
- **Type:** number
- **Required:** no

#### Actual Hours
- **Type:** number
- **Required:** no

#### Locked
- **Type:** boolean
- **Default:** false
- **Purpose:** restrict editing during QA

#### Overdue
- **Type:** boolean
- **Workflow-driven:** yes

---

## Native User fields to extend

Since your Origami environment supports custom user fields, recommended user custom fields are:

#### Department
- **Type:** text or enum

#### Job Title
- **Type:** text

#### Hourly Rate
- **Type:** number

#### Weekly Capacity Hours
- **Type:** number

#### QA Specialization
- **Type:** text or enum

These fields support better resource planning, future budget logic, and reporting.

---

<a id="prd-10"></a>

## [V1 Core] 10. Page Catalog and Visual Experience

## 1. Executive Dashboard [V1 Core]

### Purpose
Top management overview.

### Should show
- projects by status
- active epics
- tasks by status
- tasks in QA
- overdue tasks
- budget planned vs used
- progress by project

### Visual concept

```text
┌──────────────── Dashboard ────────────────┐
│ Projects Active       | 8                 │
│ Tasks In QA           | 14                │
│ Overdue Tasks         | 5                 │
│ Budget Used           | 320 / 500         │
├───────────────────────────────────────────┤
│ [Chart] Projects by Status                │
│ [Chart] Tasks by Status                   │
│ [Chart] Budget Planned vs Used            │
└───────────────────────────────────────────┘
```

---

## 2. Projects List [V1 Core]

### Purpose
One table for all projects.

### Columns
- Name
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

### Visual concept

```text
[Name] [PM] [Delivery Manager] [Delivery Team] [QA Manager] [QA Team] [Status] [Dates] [Budget] [Progress]
```

---

## 3. Project Details [V1 Core]

### Purpose
Main PM page.

### Visual concept

```text
┌────────────────────────────────────────────┐
│ Project: Smart PM System                   │
│ PM: Mor   Delivery Mgr: Dana   QA Mgr: Lee │
│ Delivery Team: Platform Devs               │
│ QA Team: Core QA                           │
│ Status: Active     Budget: 180 / 320       │
│ Dates: 01/04 → 30/06     Progress: 46%     │
├────────────────────────────────────────────┤
│ Goal                                       │
│ Build a smart Origami-based PM platform    │
├────────────────────────────────────────────┤
│ Business Context                           │
│ Need one place for planning, QA, gantt...  │
├────────────────────────────────────────────┤
│ Epics                                      │
│ - Gantt                                    │
│ - Workflow                                 │
│ - Reporting                                │
├────────────────────────────────────────────┤
│ Tasks                                      │
│ - Build project entity                     │
│ - Add QA flow                              │
└────────────────────────────────────────────┘
```

---

## 4. Epic Board [V1 Core]

### Purpose
Feature/workstream management.

### View
Kanban by epic status:

```text
Open | In Progress | Ready for QA | QA | Done
```

---

## 5. Task Board [V1 Core]

### Purpose
Execution board.

### View
Kanban by task status:

```text
New | In Progress | Ready for QA | QA | Done
```

---

## 6. Gantt / Timeline Page [V2 Advanced]

### Purpose
Project-manager visual planning.

Use it mainly for:

- Projects
- Epics

### Visual concept

```text
Project A  ━━━━━━━━━━━━━━━━━━━
  Epic 1   ━━━━━━━
  Epic 2       ━━━━━━━━━
Project B      ━━━━━━━━━━━━━━━
  Epic 3       ━━━━━
```

### Version 1 of Gantt
- show name
- owner
- start date
- end date
- status color

### Version 2
- dependencies
- milestones
- delay indicators

---

## 7. My Tasks [V1 Core]

### Purpose
Personal execution page.

### Filter
- Assignee = current user

---

## 8. QA Queue [V1 Core]

### Purpose
Pending validation work.

### Filter
- Task status = Ready for QA or QA
- Epic status = Ready for QA or QA

---

## 9. QA Team Board [V2 Advanced]

### Purpose
Separate Kanban page for QA team.

Use epic-level QA statuses:

```text
Ready for QA | QA | Done
```

This page gives the QA manager one clear place to see which epics entered QA, who owns them, and what remains open.

---

<a id="prd-11"></a>

## [V1 Core] 11. Workflow Catalog

## WF-01 — Task default values [V1 Core]

When a task is created:
- Status = New
- Locked = false
- Overdue = false

## WF-02 — Task QA lock [V1 Core]

When Task status becomes QA:
- Locked = true

Only QA Members, QA Managers, Project Managers, and System Managers may edit locked tasks.

## WF-03 — Task unlock [V1 Core]

When Task status changes from QA to another value:
- Locked = false

## WF-04 — Overdue flag [V1 Core]

When Due Date is earlier than today and Status is not Done:
- Overdue = true

Optional action:
- send notification to Project Manager

## WF-05 — Project budget rollup [V1 Core]

When Task.Actual Hours changes:
- recalculate Project.Budget Used

Version 1 formula:

```text
Budget Used = sum of related task Actual Hours
```

## WF-06 — Epic progress rollup [V1 Core]

When task status changes:
- update Epic.Progress %

## WF-07 — Project progress rollup [V1 Core]

When epic progress changes:
- update Project.Progress %

## WF-08 — Epic QA routing mail [V2 Advanced]

When an Epic status becomes Ready for QA:
- send email notification to QA Manager
- include epic name, project name, owner, dates, and link
- optionally assign epic QA owner or create a follow-up QA task

---

<a id="prd-12"></a>

## [V1 Core] 12. Notifications and QA Flow

At the **task level**, each task may have its own QA owner or task-level QA accountability.

At the **epic level**, the QA team handles validation as a grouped business process.

### Epic QA flow

1. Developer or owner moves Epic to `Ready for QA`
2. Workflow sends email to `QA Manager`
3. QA Manager reviews the incoming Epic
4. QA Manager assigns QA team member
5. Epic moves to `QA`
6. QA team member tests and either:
   - moves Epic to `Done`
   - returns it to `In Progress`

This creates a proper separation between execution and validation and is appropriate for a medium-size team with a dedicated QA function.

---

<a id="prd-13"></a>

## [V1 Core] 13. Budget and Timeline Logic

The simplest version should treat **time as the first budget unit**.

### Version 1
- `Budget Planned` = planned effort budget
- `Budget Used` = actual effort consumed

Formula:

```text
Project.Budget Used = sum(Task.Actual Hours)
```

### Version 2
Since you can extend native users, later you may add:

```text
Task Cost = Actual Hours × User.Hourly Rate
Project Budget Used = sum(Task Cost)
```

That should be a later enhancement, not a mandatory first release.

---

<a id="prd-14"></a>

## [V2 Advanced] 14. Gantt / Timeline Experience

The Gantt page should be described as a management page for:

- schedule visibility
- sequence understanding
- overlapping work detection
- delay awareness

Use it first for Projects and Epics, then later consider Tasks if the timeline must become more granular.

---

<a id="prd-15"></a>

## [V2 Advanced] 15. QA Team Board

A separate QA board is recommended when QA is run by its own team.

This board should show:
- Epic
- Project
- QA Owner
- Current QA status
- related open tasks
- overdue QA items

---

<a id="prd-16"></a>

## [V2 Advanced] 16. Reporting and Dashboards

Later reports can include:
- budget by manager or team
- epic cycle time
- overdue trends
- QA lead time
- workload by user
- project velocity

---

<a id="prd-17"></a>

## [V3 Optional] 17. Future Enhancements

- cost-based budget using user hourly rate
- dependency lines in Gantt
- automatic next-task creation
- team capacity warnings
- client-facing portal/reporting
- risk register
- milestone management

---

### Other documents
- [← README — how to use this documentation](README.md)
- [Build Guide — Origami implementation →](BUILD_GUIDE.md)
