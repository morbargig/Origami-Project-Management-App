# Permissions

## Principle

Permissions should mirror delivery accountability. The system should be open enough for execution and strict enough for QA and governance.

## Access Model

### System Managers
- full access to all entities and pages

### Project Managers
- full access to Projects, Epics, and Tasks
- edit budget and timeline fields
- see all operational and management pages

### Developers / Team Members
- view projects and epics
- edit assigned tasks
- update actual hours
- move task statuses through allowed steps

### QA Managers
- see QA views
- edit epics and tasks inside QA flow
- receive QA routing notifications
- assign QA Members

### QA Members
- edit QA-assigned work
- move work through QA statuses

### Viewers
- read-only access

## Locked Task Rule

When a task enters `Self QA`, editing should be restricted to:
- `Assignee`
- `QA Assignee`
- Project Managers
- System Managers
