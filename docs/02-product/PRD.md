# Product Requirements Document (PRD) — JiraGami

**Documentation order:** [README](../../README.md) -> **Product Requirements Document (PRD) (this file)** -> [Build Guide](../03-implementation/BUILD_GUIDE.md)

## Purpose

This Product Requirements Document (PRD) is the canonical product-definition document for `JiraGami`, a Smart Project Management product deployed on the `Origami` platform.

It defines why the system exists, what it contains, how the entity model works, how Quality Assurance (QA) is structured, and what the main user-facing pages should do.

The Build Guide defines how to implement the same model in Origami.

## Executive Summary

Origami Smart PM is a smart project management system built on Origami for medium-size teams.

Its purpose is to help managers define project goals clearly, break work into structured levels, manage execution, track time and budget simply, and control delivery through permissions, workflows, and visual pages.

This is not only a task board. It is a project-management operating model based on:
- context
- time
- resources
- budget
- quality gates
- manager visibility

## Project Management Mindset

Context -> Goal -> Plan -> Execution -> Quality Assurance (QA) -> Delivery

Inside the system:

Project -> Epic -> Task

Each system part maps directly to a project-management concept:
- Business Context = why the project exists
- Project Goal = what success looks like
- Dates / Gantt chart = time planning
- Users / Teams / Quality Assurance (QA) = resources and responsibility
- Budget fields = cost control
- Quality Assurance (QA) flow = quality control
- Dashboards = governance and visibility

## Product Vision

The vision is to create a single Origami workspace where a manager can:
- define a project clearly
- connect the project to a responsible team
- divide the project into epics
- divide epics into tasks
- send work through controlled Quality Assurance (QA) stages
- monitor timeline visually
- track budget simply
- give each team the right page and permissions

## Platform Principles

Origami Smart PM is built on Origami and intentionally uses:
- native Origami Users
- native Origami Groups
- native Origami metadata fields
- Origami workflows
- Origami pages, boards, Gantt chart, and dashboard capabilities
- custom user fields on native Origami Users

Important Origami constraint:
- custom fields cannot point to a Group
- project staffing must use `user` and `multi-user` fields
- project staffing must not be modeled with group custom fields

## Target Users

- Project Managers
- Delivery Managers
- Developers / Team Members
- Quality Assurance (QA) Teams
- Stakeholders / Clients / Managers

## Scope

Version 1 includes:
- Projects
- Epics
- Tasks
- native Origami users and groups
- native metadata fields
- Gantt chart / timeline page
- Task Kanban board
- Epic Kanban board
- Quality Assurance (QA) Kanban board
- Dashboard
- Budget tracking
- Notifications
- Workflows

Version 1 does not require deep Enterprise Resource Planning (ERP) financial logic, billing complexity, or advanced dependency engines.

## Core Structure

Project -> Epic -> Task

- Project = manager level
- Epic = workstream or major deliverable
- Task = execution level

Diagram: [`../../assets/diagrams/system-architecture.svg`](../../assets/diagrams/system-architecture.svg)

## Teams, Ownership, and Quality Assurance (QA) Structure

This system should use Origami native Users and Groups.

Recommended groups:
- System Managers
- Project Managers
- Developers / Team Members
- QA Managers
- QA Members
- Viewers

Each Project should have:
- a `Project Manager`
- a `Delivery Manager`
- a `Delivery Team`
- a `QA Manager`
- a `QA Team`

## Entity Catalog

### Project

Purpose: the main management record for initiative context, goal, time frame, ownership, staffing, and budget.

Fields:
- `Name` — text
- `Description` — long text
- `Project Goal` — long text
- `Business Context` — long text
- `Project Manager` — user
- `Delivery Manager` — user
- `Delivery Team` — multi-user
- `QA Manager` — user
- `QA Team` — multi-user
- `Status` — enum
- `Start Date` — date
- `End Date` — date
- `Budget Planned` — number
- `Budget Used` — number, workflow-driven
- `Progress %` — number, workflow-driven

Status values:
- Draft
- Active
- On Hold
- Completed
- Archived

### Epic

Purpose: a major stream of work under a project.

Fields:
- `Title` — text
- `Project` — relation to Project
- `Description` — long text
- `Goal` — long text
- `Owner` — user
- `QA Owner` — user
- `Status` — enum
- `Start Date` — date
- `End Date` — date
- `Progress %` — number, workflow-driven

Status values:
- Open
- In Progress
- Ready for QA
- QA
- Done

### Task

Purpose: the execution unit assigned to a specific person.

Fields:
- `id` — auto-id / readonly
- `Title` — text
- `Description` — long text
- `Project` — relation to Project
- `Epic` — relation to Epic
- `Assignee` — user
- `QA Assignee` — user, optional
- `Status` — enum
- `Priority` — enum
- `Due Date` — date
- `Start Date` — date
- `Estimated Hours` — number
- `Actual Hours` — number
- `Locked` — boolean
- `Overdue` — boolean, workflow-driven

Status values:
- New
- InProgress
- Self QA
- Done

Priority values:
- Low
- Medium
- High
- Critical

## Task Responsibility Rule

This rule is critical and must remain intact:
- `Assignee` is always responsible for making sure the task is actually done
- by default, the `Assignee` also validates the task
- `QA Assignee` is optional
- `QA Assignee` is only used when a second review is needed
- while the Epic is `In Progress`, `QA Assignee` is only a reviewer and does not own task status updates
- the reviewer confirms readiness outside the workflow
- the `Assignee` updates the task status
- formal routed Quality Assurance (QA) is primarily handled at the Epic level

## Quality Assurance (QA) Model

### Task level
- lightweight validation
- default self-validation by `Assignee`
- optional `QA Assignee` reviewer
- task status flow: `New -> InProgress -> Self QA -> Done`

### Epic level
- formal Quality Assurance (QA) flow
- epic status flow: `Open -> In Progress -> Ready for QA -> QA -> Done`
- when Epic becomes `Ready for QA`, `QA Manager` should receive notification or email
- Quality Assurance (QA) team handles formal QA routing

Diagram: [`../../assets/diagrams/qa-flow.svg`](../../assets/diagrams/qa-flow.svg)

## Workflow Baseline

### WF-01 Task default values
- on task creation
- set `Status = New`
- set `Locked = false`
- set `Overdue = false`

### WF-02 Task validation lock
- when `Task.Status` becomes `Self QA`
- set `Locked = true`
- restrict editing to:
  - `Assignee`
  - `QA Assignee`
  - `Project Managers`
  - `System Managers`

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

### WF-08 Epic Quality Assurance (QA) routing email
- when `Epic.Status` changes to `Ready for QA`
- send email to `QA Manager`
- include Epic, Project, Owner, dates, and link
- optionally set `QA Owner` or create QA follow-up action

## Current Page Baseline

### Executive Dashboard
- projects by status
- active epics
- tasks by status
- tasks in Quality Assurance (QA)
- overdue tasks
- budget planned vs used
- progress by project

### Projects List
- main projects table

### Project Details
- Project Manager (PM) main page
- summary + goal + context + epics + tasks + staffing + budget

### Epic Board
- Kanban board by epic status: `Open | In Progress | Ready for QA | QA | Done`

### Task Board
- Kanban board by task status: `New | InProgress | Self QA | Done`

### My Tasks
- filter by `Assignee = current user`

### QA Queue (Quality Assurance Queue)
- task status = `Self QA`
- epic status = `Ready for QA` or `QA`

### Gantt Chart / Timeline
- mostly Project + Epic timeline
- not overloaded with task-level bars in version 1

### QA Team Board (Quality Assurance Team Board)
- epic-level Kanban board: `Ready for QA | QA | Done`

Diagram: [`../../assets/diagrams/pages-structure.svg`](../../assets/diagrams/pages-structure.svg)

## User Custom Fields

Native Origami Users are extendable in this environment. Recommended user fields:
- `Mobile Number`
- `Department`
- `Job Title`
- `Hourly Rate`
- `Weekly Capacity Hours`
- `Specialization`
