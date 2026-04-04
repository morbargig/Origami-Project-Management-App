# Scope Baseline

## Purpose

This scope baseline defines what the `JiraGami` documentation and governance layer may change and what it must preserve.

## In Scope

- executive framing and product explanation
- Product Requirements Document (PRD) positioning and navigation
- implementation and operations documentation alignment
- governance and reporting documents for managers
- terminology and identity standardization
- canonical-source rules
- stakeholder communication structure

## Out Of Scope

- product behavior changes
- workflow redesign
- status changes
- entity or field changes
- permissions logic changes
- page behavior changes
- changes to production meaning disguised as documentation edits

## Assumptions

- `JiraGami` already has a defined live product baseline
- the current PRD and Build Guide reflect the intended production truth
- documentation should support management, not redesign the product
- existing field names and workflow terms must remain exact where they describe product behavior

## Constraints

- the product model must remain unchanged unless canonical product docs are intentionally updated first
- the documentation set must stay internally consistent
- governance docs must remain lightweight and useful
- summary documents must never become an alternate source of product truth

## Scope Control Rule

If a future change would alter product truth, it must be handled in the canonical product or implementation documents first, and only then reflected in overview or governance summaries.
