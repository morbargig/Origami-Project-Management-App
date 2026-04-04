# JiraGami

Professional project documentation for `JiraGami`.

## Project Identity

`JiraGami` is the project name.

`JiraGami` is a Smart Project Management product deployed on the `Origami` platform and influenced by Jira-style delivery practices.

This repository exists to organize the project, product, implementation, operations, and management documents in a way that looks professionally structured and owned by a Project Manager.

## Project Management Ownership

- Project Manager: `Mor Bargig`
- Project: `JiraGami`
- Product type: `Smart Project Management system`
- Deployment platform: `Origami`
- Product positioning: `Origami-based Smart PM product with Jira-inspired management structure`

## Executive Summary

This repository is the professional documentation library for the `JiraGami` project.

It is structured to help managers, delivery teams, implementers, and stakeholders understand:
- what the project is
- what the product does
- how the platform is configured
- how work is managed and validated
- how the project is governed, reported, and communicated

## Documentation Principles

- documentation changes must not change production truth
- product definitions remain separate from implementation guidance
- project management documents support the product and do not replace the canonical product baseline
- each topic must have one clear canonical source
- the repository should look like it was planned, organized, and governed by a professional Project Manager

## Core Delivery Model

Context -> Goal -> Plan -> Execution -> Quality Assurance (QA) -> Delivery

Core product structure:

Project -> Epic -> Task

## Table Of Contents

All canonical project documentation lives under `docs/`.

### Core Navigation

- [Master Table of Contents](docs/TABLE_OF_CONTENTS.md)
- [Documentation Hub](docs/README.md)

### 1. Overview

- [Vision](docs/01-overview/vision.md)
- [Mindset](docs/01-overview/mindset.md)
- [Architecture](docs/01-overview/architecture.md)

### 2. Product

- [Product Requirements Document (PRD)](docs/02-product/PRD.md)
- [Entities](docs/02-product/entities.md)
- [Workflows](docs/02-product/workflows.md)

### 3. Implementation

- [Build Guide](docs/03-implementation/BUILD_GUIDE.md)
- [Origami setup](docs/03-implementation/origami-setup.md)
- [Permissions](docs/03-implementation/permissions.md)

### 4. Views

- [Dashboard](docs/04-views/dashboard.md)
- [Gantt chart](docs/04-views/gantt.md)
- [Boards](docs/04-views/boards.md)
- [Pages](docs/04-views/pages.md)

### 5. Operations

- [Quality Assurance (QA) process](docs/05-operations/qa-process.md)
- [Delivery flow](docs/05-operations/delivery-flow.md)
- [Budget model](docs/05-operations/budget-model.md)

### 6. Project Management

- [Project Management README](docs/06-governance/README.md)
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

### 99. Exports

- [Full export](docs/99-exports/FULL_EXPORT.md)
- [Product Requirements Document (PRD) + Build merged](docs/99-exports/PRD_BUILD_MERGED.md)

## Canonical Sources

Use these files as the primary truth for the live product and project model:
- product definition: `docs/02-product/PRD.md`
- implementation design: `docs/03-implementation/BUILD_GUIDE.md`
- page and view baseline: `docs/04-views/pages.md`
- operating model: `docs/05-operations/`
- project management control documents: `docs/06-governance/`

Project management documents must support the live product and must not rewrite the production baseline.

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
2. `docs/TABLE_OF_CONTENTS.md`
3. `docs/06-governance/PDR.md`
4. `docs/02-product/PRD.md`

For implementation planning:
1. `docs/02-product/PRD.md`
2. `docs/03-implementation/BUILD_GUIDE.md`
3. `docs/04-views/`

For project management control:
1. `docs/06-governance/PDR.md`
2. `docs/06-governance/project-charter.md`
3. `docs/06-governance/scope-baseline.md`
4. `docs/06-governance/roadmap.md`
5. `docs/06-governance/raid-log.md`
6. `docs/06-governance/project-status-report.md`

## Project Management Terms

- `Project Definition Report (PDR)` = the executive project-definition document
- `Product Requirements Document (PRD)` = the canonical product-definition document
- `Quality Assurance (QA)` = the validation and testing control layer
- `Project Manager (PM)` = the management role responsible for visibility, structure, and control
- `Gantt chart` = the management timeline view
- `Kanban board` = the board view used to track work by status
- `RAID` = risks, assumptions, issues, and dependencies
- `RACI` = responsible, accountable, consulted, and informed
- `Enterprise Resource Planning (ERP)` = deeper business-system finance logic that is out of scope for version 1
- `Artificial Intelligence (AI)` = tools such as ChatGPT and Cursor used to read and update the documentation

## Diagrams And Images

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

## Artificial Intelligence (AI) Usage

When using ChatGPT or Cursor:

1. Start with `README.md`.
2. Load `docs/02-product/PRD.md` for Product Requirements Document (PRD) truth.
3. Load `docs/03-implementation/BUILD_GUIDE.md` for Origami setup details.
4. Use the split docs for focused edits by topic.
5. Keep product changes aligned with current field names, workflow names, and Quality Assurance (QA) logic.

## Product Screenshots

- [Dashboard example](docs/04-views/dashboard.md)
- [Timeline and planning examples](docs/04-views/gantt.md)
- [Board and table examples](docs/04-views/boards.md)
- [User and group setup example](docs/03-implementation/origami-setup.md)

![Dashboard overview](assets/images/dashboard-overview.png)
