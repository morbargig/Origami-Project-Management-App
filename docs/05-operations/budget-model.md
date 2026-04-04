# Budget Model

## Version 1 Principle

This document describes the management budget model for `JiraGami` while preserving the production baseline of `Origami Smart PM`.

Time is the first budget unit.

### Core Fields
- `Budget Planned` = planned effort budget
- `Budget Used` = actual effort consumed

### Formula
- `Project.Budget Used = sum(Task.Actual Hours)`

## Version 2 Direction

Once user hourly rates are available, cost-based tracking can be added:
- `Task Cost = Actual Hours * User.Hourly Rate`
- `Project Budget Used = sum(Task Cost)`

This is a later enhancement, not a first-release requirement.
