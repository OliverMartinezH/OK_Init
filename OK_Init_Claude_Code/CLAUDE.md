# CLAUDE.md

## OK_Init - Project Governance

This project uses OK_Init governance system with 5 files:
- `Proyecto [NAME].md` - Architectural map
- `agent.md` - Coding rules + decisions
- `stack.md` - Tech stack + data model
- `progress.md` - Current state + next step
- `history.md` - Completed phases

## Commands

Use these slash commands:
- `/ok init` - Initialize or continue project
- `/ok sigamos` - Continue from where we left off
- `/ok sync` - Audit MD vs code
- `/ok status` - Show dashboard
- `/ok commit` - Commit changes

## Rules

- Files are only updated AFTER user approval
- Never delete entries from MD (mark as "Not built")
- Use Obsidian wiki-links between files
- Date format: DD/MM/YYYY HH:MM (America/Santiago)

## Architecture

- **Core:** [ProjectName].Application — Use cases and services
- **Data:** [ProjectName].Infrastructure — Database and repositories
- **Presentation:** [ProjectName].Web — Controllers and views
- **Tests:** tests/[ProjectName].Tests — Unit tests

## Coding Standards

- Use Result pattern for error handling (no exceptions)
- Every new feature MUST have unit tests
- Method naming: [Method]_[Scenario]_[ExpectedResult]
- KISS principle: simplicity first
