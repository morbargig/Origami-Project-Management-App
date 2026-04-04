# JiraGami

Professional documentation for the live `JiraGami` product.

## Product Identity

`JiraGami` is a Smart Project Management product deployed on the `Origami` platform.

It is designed for teams that need more than a task board: clear project context, structured execution, visible timelines, formal Quality Assurance (QA) routing, and management-friendly reporting.

This repository organizes the product, implementation, operations, and governance documentation around the live product model.

## What This Repository Covers

This documentation set helps readers understand:
- what `JiraGami` is
- how the product model works
- how the system should be configured in Origami
- how delivery and Quality Assurance (QA) are operated
- how the project is governed, reported, and communicated

## Production-Safe Documentation Rules

- documentation must not silently change production truth
- product definition, implementation guidance, operations, and governance stay separate
- each major topic should have one clear canonical source
- summary documents support the product and do not replace canonical baselines
- governance content should improve clarity, not invent a different product

## Core Delivery Model

Context -> Goal -> Plan -> Execution -> Quality Assurance (QA) -> Delivery

Core product structure:

Project -> Epic -> Task

## Canonical Sources

Use these files as the primary truth for the live product model:
- product definition: `docs/02-product/PRD.md`
- implementation design: `docs/03-implementation/BUILD_GUIDE.md`
- page and view baseline: `docs/04-views/pages.md`
- operating model: `docs/05-operations/`

Project management documents in `docs/06-governance/` support planning, reporting, and control, but they must not redefine the product baseline.

## Documentation Map

All primary documentation lives under `docs/`.

### Start Here

- [Documentation Hub](docs/README.md)
- [Master Table of Contents](docs/TABLE_OF_CONTENTS.md)

### Overview

- [Vision](docs/01-overview/vision.md)
- [Mindset](docs/01-overview/mindset.md)
- [Architecture](docs/01-overview/architecture.md)

### Product

- [Product Requirements Document (PRD)](docs/02-product/PRD.md)
- [Entities](docs/02-product/entities.md)
- [Workflows](docs/02-product/workflows.md)

### Implementation

- [Build Guide](docs/03-implementation/BUILD_GUIDE.md)
- [Origami setup](docs/03-implementation/origami-setup.md)
- [Permissions](docs/03-implementation/permissions.md)

### Views

- [Dashboard](docs/04-views/dashboard.md)
- [Gantt chart](docs/04-views/gantt.md)
- [Boards](docs/04-views/boards.md)
- [Pages](docs/04-views/pages.md)

### Operations

- [Quality Assurance (QA) process](docs/05-operations/qa-process.md)
- [Delivery flow](docs/05-operations/delivery-flow.md)
- [Budget model](docs/05-operations/budget-model.md)

### Governance

- [Governance README](docs/06-governance/README.md)
- [Project Definition Report (PDR)](docs/06-governance/PDR.md)
- [Project Charter](docs/06-governance/project-charter.md)
- [Scope Baseline](docs/06-governance/scope-baseline.md)
- [Roadmap](docs/06-governance/roadmap.md)
- [RAID Log](docs/06-governance/raid-log.md)
- [RACI Matrix](docs/06-governance/raci.md)
- [Communication Plan](docs/06-governance/communication-plan.md)
- [Project Status Report](docs/06-governance/project-status-report.md)
- [Decision Log](docs/06-governance/decision-log.md)
- [Success Metrics](docs/06-governance/success-metrics.md)

### Exports

- [Full export](docs/99-exports/FULL_EXPORT.md)
- [Product Requirements Document (PRD) + Build merged](docs/99-exports/PRD_BUILD_MERGED.md)

## Audience

- Project Managers
- Delivery Managers
- Product and implementation leads
- Developers
- Quality Assurance (QA) teams
- Stakeholders and clients
- Artificial Intelligence (AI) tools such as ChatGPT and Cursor

## Recommended Reading Paths

For executive understanding:
1. `README.md`
2. `docs/01-overview/vision.md`
3. `docs/06-governance/PDR.md`
4. `docs/02-product/PRD.md`

For implementation planning:
1. `docs/02-product/PRD.md`
2. `docs/03-implementation/BUILD_GUIDE.md`
3. `docs/04-views/pages.md`
4. `docs/05-operations/qa-process.md`

For governance and reporting:
1. `docs/06-governance/PDR.md`
2. `docs/06-governance/project-charter.md`
3. `docs/06-governance/scope-baseline.md`
4. `docs/06-governance/roadmap.md`
5. `docs/06-governance/raid-log.md`
6. `docs/06-governance/project-status-report.md`

## Working Terms

- `Project Definition Report (PDR)` = executive project framing and management context
- `Product Requirements Document (PRD)` = canonical product-definition document
- `Quality Assurance (QA)` = the validation and testing control layer
- `Project Manager (PM)` = the management role responsible for visibility, structure, and control
- `Gantt chart` = the management timeline view
- `Kanban board` = the board view used to track work by status
- `RAID` = risks, assumptions, issues, and dependencies
- `RACI` = responsible, accountable, consulted, and informed
- `Enterprise Resource Planning (ERP)` = deeper finance logic that is out of scope for version 1

## Diagrams And Screenshots

All diagrams are stored under `assets/diagrams/`.

Concept and structure:
- [System architecture](assets/diagrams/system-architecture.svg)
- [Pages structure](assets/diagrams/pages-structure.svg)

Workflow and delivery control:
- [Quality Assurance (QA) flow](assets/diagrams/qa-flow.svg)

Timeline and planning:
- [Gantt chart logic](assets/diagrams/gantt-logic.svg)

Setup and ownership:
- [Build order](assets/diagrams/build-order.svg)
- [Project ownership](assets/diagrams/project-ownership.svg)

Screenshots live under `assets/images/` and are embedded into the relevant docs.

### Inline Diagram Preview

#### System architecture

![System architecture](assets/diagrams/system-architecture.svg)

#### Quality Assurance (QA) flow

![QA flow](assets/diagrams/qa-flow.svg)

#### Gantt chart logic

![Gantt logic](assets/diagrams/gantt-logic.svg)

#### Pages structure

![Pages structure](assets/diagrams/pages-structure.svg)

## AI Usage

When using ChatGPT or Cursor:

1. Start with `README.md`.
2. Use `docs/02-product/PRD.md` as the product truth.
3. Use `docs/03-implementation/BUILD_GUIDE.md` for Origami configuration details.
4. Use split docs for focused edits by topic.
5. Keep any summary or governance changes aligned with the live product model.

## Product Screenshots

- [Dashboard example](docs/04-views/dashboard.md)
- [Timeline and planning examples](docs/04-views/gantt.md)
- [Board and table examples](docs/04-views/boards.md)
- [User and group setup example](docs/03-implementation/origami-setup.md)

![Dashboard overview](assets/images/dashboard-overview.png)
