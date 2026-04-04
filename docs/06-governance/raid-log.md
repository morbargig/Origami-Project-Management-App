# RAID Log

## Purpose

This document tracks management-level `Risks`, `Assumptions`, `Issues`, and `Dependencies` for the documentation and governance layer.

## Risks

- documentation duplication could confuse stakeholders about the canonical source
- future edits could unintentionally change wording that represents production truth
- governance documents could become outdated if not maintained with the canonical docs

## Assumptions

- the product model described in the Product Requirements Document (PRD) is valid
- implementation guidance reflects the live platform baseline
- stakeholders need both detailed product documents and executive-level summaries

## Issues

- some current topics are repeated across overview, product, and implementation files
- manager-facing governance artifacts were previously missing from the repository
- export files are lighter than their names currently suggest

## Dependencies

- governance docs depend on the Product Requirements Document (PRD) staying authoritative
- implementation documentation depends on the Build Guide staying authoritative
- manager reporting depends on dashboard, budget, workflow, and page documents remaining aligned

## Review Cadence

Review this log whenever:
- canonical product documents change
- major governance documents are added or updated
- new product assumptions or delivery risks appear
