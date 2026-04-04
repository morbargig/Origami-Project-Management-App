# Architecture

## System Architecture

Origami Smart PM is structured around one core hierarchy:

Project -> Epic -> Task

This hierarchy is the operational backbone of the system.

- `Project` is the manager-level record.
- `Epic` is the workstream or major deliverable.
- `Task` is the execution-level work item.

## Platform Building Blocks

The system is built using:
- native Origami Users
- native Origami Groups
- native Origami metadata fields
- custom user fields on native Origami Users
- Origami workflows
- Origami pages, boards, gantt, and dashboard views

## Staffing Constraint

Origami custom fields cannot point to a Group.

Therefore project staffing must use:
- `user` fields
- `multi-user` fields

Project staffing must not be modeled with group custom fields.

## Control Layers

The architecture includes these control layers:
- entity structure through Project, Epic, and Task
- responsibility structure through managers, teams, assignees, and QA roles
- workflow control through task and epic automation
- management visibility through Dashboard, Boards, and Gantt

## Diagrams

- [System architecture](../../assets/diagrams/system-architecture.drawio)
- [QA flow](../../assets/diagrams/qa-flow.drawio)
