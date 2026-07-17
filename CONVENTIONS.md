# OK_Init Governance Conventions

## Session Start
Read these files for context:
- `agent.md` → Coding rules and decisions
- `progress.md` → Current phase and next step
- `stack.md` → Technical decisions

## Rules
- Follow the phase order defined in `progress.md`
- Generate code ONLY for the current step
- If ambiguous, ask the user before writing code
- Minor dependencies: create stub with `// TODO: Implement in corresponding step`
- Update files ONLY after user approval

## Workflow Commands
- `ok init` → Initialize governance files
- `ok sigamos` → Continue from where we left off
- `ok sync` → Audit MD files vs actual code
- `ok status` → Show project status dashboard
- `ok commit` → Commit governance + code with questions
