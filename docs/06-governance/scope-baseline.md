# Scope Baseline

## Purpose

This scope baseline defines the documentation scope for the `JiraGami` management layer for the `JiraGami` product on the `Origami` platform.

## In Scope

- executive project framing
- Product Requirements Document (PRD) positioning and navigation
- implementation and operations documentation alignment
- governance and reporting documents for managers
- terminology standardization
- canonical-source rules
- stakeholder communication structure

## Out Of Scope

- product behavior changes
- workflow redesign
- status changes
- entity or field changes
- permissions logic changes
- page behavior changes
- diagram meaning changes beyond wording and navigation context

## Assumptions

- `JiraGami` already has a defined product baseline
- the current PRD and Build Guide reflect the intended production baseline
- documentation should support management, not redesign the product
- existing field names and workflow terms must remain exact where they describe production truth

## Constraints

- the product model must remain unchanged
- the documentation must stay internally consistent
- governance docs must be lightweight and useful, not bureaucratic overhead
- new PM artifacts must support the current delivery model rather than inventing a different one

## Scope Control Rule

If a future documentation change would alter product truth, that change must be handled in the canonical product or implementation documents first, not in governance summaries.
