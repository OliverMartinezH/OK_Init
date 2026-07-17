# OK_Init — Project Governance Skill

> **For [opencode](https://opencode.ai)** — Generate a complete governance system for any project with Obsidian wiki-links and a KISS workflow protocol.

[![Obsidian](https://img.shields.io/badge/Obsidian-ready-7C3AED?style=flat-square&logo=obsidian)](https://obsidian.md)
[![opencode](https://img.shields.io/badge/opencode-000000?style=flat-square)](https://opencode.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

---

## What is OK_Init?

OK_Init generates **5 governance files** that act as a knowledge base for your project. These files are:

- **Obsidian-ready** with `[[wiki-links]]` between them
- **Self-updating** as your project evolves
- **Tech-agnostic** — works with .NET, Node.js, Python, or anything

### The 5 Files

| File | Purpose | Obsidian Link |
|------|---------|---------------|
| `Proyecto [NAME].md` | Architectural map of your project | Links to all other files |
| `agent.md` | Coding rules + decision history | `[[stack]]` `[[progress]]` |
| `stack.md` | Tech stack + data model + UI standard | `[[agent]]` `[[progress]]` |
| `progress.md` | Current state + next step | `[[history]]` `[[stack]]` |
| `history.md` | Accumulated memory of completed phases | `[[progress]]` |

---

## Obsidian Integration

### How It Works

Each file starts with wiki-links to the other files:

```markdown
# Agent Instructions: MyProject

> **Map:** Ver [[Proyecto MyProject]]
> **Stack:** Ver [[stack]]
> **Status:** Ver [[progress]]
> **History:** Ver [[history]]
```

### Graph View in Obsidian

This creates an interactive graph in Obsidian:

```
┌──────────────────┐
│  Proyecto        │
│  MyProject       │
└────────┬─────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌────────┐ ┌────────┐
│ stack  │ │ agent  │
│ (tech) │ │ (rules)│
└───┬────┘ └───┬────┘
    │          │
    ▼          ▼
┌────────┐ ┌────────┐
│progress│ │ history│
│ (state)│ │ (mem)  │
└────────┘ └────────┘
```

Click any `[[link]]` to navigate between files. Obsidian automatically shows the relationship graph.

### Callouts

The generated files use Obsidian callouts for visual emphasis:

| Callout | Usage |
|---------|-------|
| `> [!note]` | General information |
| `> [!tip]` | Helpful tips and recommendations |
| `> [!warning]` | Important rules and constraints |
| `> [!important]` | Critical architectural decisions |

Example:

```markdown
> [!tip] First step
> Start with Phase 0: Testing Infrastructure.
> Create the test project and validate the Result pattern.
```

### Tags

Files include tags for filtering in Obsidian:

- `#fase/0`, `#fase/1`, `#fase/2` — Phase tags
- `#modulo/NOMBRE` — Module tags (if applicable)

---

## Quick Start

### Installation

**Global (all projects):**

```bash
# Copy to global skills directory
cp ok-init.md ~/.config/opencode/skills/
```

**Local (single project):**

```bash
# Copy to your project's .opencode directory
mkdir -p .opencode/skills
cp ok-init.md .opencode/skills/
```

### Usage

Type any of these triggers in opencode:

| Command | Action |
|---------|--------|
| `ok init` | Detect files → continue or generate |
| `ok sigamos` | Same as `ok init` |
| `ok sync` | Audit MD vs actual code |
| `ok status` | Show project status dashboard |
| `ok commit` | Commit governance + code (with questions) |

### Smart Detection

The skill automatically detects if governance files already exist:

```
ok init
    │
    ├── Files exist?
    │   ├── YES → Read state → Continue working
    │   └── NO → New project?
    │       ├── Ask all → 6 questions → Generate
    │       └── Use context → Summarize chat → Generate
    │
    └── Session Protocol
```

### Continue an Existing Project

If you open a new window in a project that already has governance files:

```
USUARIO: ok sigamos

AI: [reads progress.md, agent.md, stack.md]
AI: We're in Phase 2.1 - Creating domain entities.
    Next step: Create Client entity with RUT, Name, Email.
    Shall I proceed?
```

No menus. No questions. Just continue.

### "Use Context" Mode

If you've been chatting about your project and then invoke the skill:

```
You: [chatting about your project...]
You: ok init

AI: No governance files found.
    Want me to generate them based on our conversation?

You: yes

AI: Here's what I captured:
    - Project: NexusPlatform
    - Stack: .NET 10
    - Database: SQL Server 2022
    - Testing: xUnit
    - UI: Tailwind CDN
    - Auth: Cookie

    Is this correct?

You: yes

AI: [generates 5 files]
```

---

## Commands

### `ok init` / `ok sigamos`

Detect if governance files exist and either continue or generate new ones.

```
ok init
    │
    ├── Files exist?
    │   ├── YES → Read state → Continue working
    │   └── NO → New project?
    │       ├── Ask all → 6 questions → Generate
    │       └── Use context → Summarize chat → Generate
    │
    └── Session Protocol
```

### `ok sync`

Audit governance files against actual code. **Never deletes entries** — marks them as "Not built" instead.

```
📊 Sync Report - NexusPlatform

✅ Synced (12):
- Phase 1: Core (complete)
- Entity: Client

➕ New in code (3):
- src/Services/PaymentService.cs

⏸️ Pending - Not built (2):
- progress.md: "3.2 Add validation" → code doesn't exist
```

### `ok status`

Show a visual dashboard of the project status.

```
📊 NexusPlatform - Estado del Arte

Progreso: ████████░░░░░░░░░░░░ 40% (10/25)
Fase actual: 2 - Business Logic
Última sesión: 16/07/2026 - Phase 1 completed
Próximo paso: 2.1 Create domain entities
```

### `ok commit`

Commit governance files and code with interactive questions.

```
📝 Governance (2 archivos):
- progress.md (modificado)
- agent.md (modificado)

💻 Código (3 archivos):
- src/Services/PaymentService.cs (nuevo)
- src/Controllers/WebhookController.cs (modificado)
- tests/PaymentTests.cs (nuevo)

¿Qué quieres commitear?
1. Governance
2. Código
3. Ambos
4. No
```

**Auto-suggested messages:**
- Governance only → `docs: update governance files`
- Code only → `feat: [based on files]`
- Both → `feat: [code summary] + docs: governance update`

---

## Questions Asked

| # | Question | Default |
|---|----------|---------|
| 1 | Project name | *(required)* |
| 2 | Tech stack | `.NET 10 + C# 14` |
| 3 | Database | `SQL Server 2022` |
| 4 | Testing framework | `xUnit + Moq` |
| 5 | UI framework | `Tailwind CDN` |
| 6 | Auth strategy | `Cookie Authentication` |

Press **Enter** to accept the default, or type your own.

---

## Session Protocol

### Start of Session

1. Read `progress.md` → current phase and next step
2. Read `agent.md` → rules and decisions
3. Read `stack.md` → technical decisions

### During Session

- Generate code **only for the current step**
- If ambiguous, **ask before coding**
- Minor dependencies: create stub with `// TODO`

### End of Session (after user approval)

1. `progress.md` → mark completed + set next step
2. `history.md` → move phase with date (DD/MM/YYYY HH:MM)
3. `stack.md` → document new technical decisions
4. `agent.md` → document new rules/decisions

> **Golden rule:** Files are **only updated AFTER user approval**.

---

## File Structure

```
your-project/
├── Proyecto [YOUR_PROJECT].md
├── agent.md
├── stack.md
├── progress.md
├── history.md
└── opencode.json (if not exists)
```

---

## Example Output

### `agent.md` (excerpt)

```markdown
# Agent Instructions: NexusPlatform

> **Map:** Ver [[Proyecto NexusPlatform]]
> **Stack:** Ver [[stack]]
> **Status:** Ver [[progress]]

---

## 1. Development Philosophy

* **KISS:** Extreme simplicity
* **Result Pattern:** No exceptions for business validations
* **Auth:** Cookie + PasswordHasher

---

## 2. Decision History

> [!note] Session history
> This space fills automatically during development.

* Pending first session.
```

### `stack.md` (excerpt)

```markdown
# Tech Stack: NexusPlatform

> **Map:** Ver [[Proyecto NexusPlatform]]
> **Rules:** Ver [[agent]]

---

## 1. Technologies

* **Runtime:** .NET 10 + C# 14
* **Database:** SQL Server 2022
* **UI:** Tailwind CDN
* **Testing:** xUnit + Moq
```

---

## Requirements

- [opencode](https://opencode.ai) installed
- Obsidian (optional, for graph views)

---

## License

MIT

---

# Spanish

## Qué es OK_Init?

OK_Init genera **5 archivos de gobernanza** que actúan como base de conocimiento para tu proyecto. Estos archivos son:

- **Listos para Obsidian** con `[[wiki-links]]` entre ellos
- **Auto-actualizables** a medida que evoluciona tu proyecto
- **Independientes del stack** — funciona con .NET, Node.js, Python, o cualquier tecnología

### Los 5 Archivos

| Archivo | Propósito | Enlace Obsidian |
|---------|-----------|-----------------|
| `Proyecto [NOMBRE].md` | Mapa arquitectónico del proyecto | Enlaza a todos los demás |
| `agent.md` | Reglas de código + historial de decisiones | `[[stack]]` `[[progress]]` |
| `stack.md` | Stack técnico + modelo de datos + estándar UI | `[[agent]]` `[[progress]]` |
| `progress.md` | Estado actual + próximo paso | `[[history]]` `[[stack]]` |
| `history.md` | Memoria acumulativa de fases completadas | `[[progress]]` |

---

## Triggers

| Trigger | Acción |
|---------|--------|
| `ok init` | Detectar archivos → continuar o generar |
| `ok sigamos` | Igual que `ok init` |
| `ok sync` | Auditar MD vs código real |
| `ok status` | Mostrar dashboard del estado del arte |
| `ok commit` | Commitear governance + código (con preguntas) |

### `ok sync` (Auditoría)

Compara los MD con el código real. **Nunca borra entradas** — las marca como "No construido".

### `ok status` (Dashboard)

Muestra un resumen visual del estado del proyecto:
- Barra de progreso
- Fase actual
- Última sesión
- Próximo paso

### `ok commit` (Commit interactivo)

Commitea archivos de governance y código con preguntas interactivas:
- Clasifica archivos (governance vs código)
- Pregunta qué commitear
- Sugiere mensaje automático o permite custom
- Ejecuta git add + commit

---

## Instalación

**Global (todos los proyectos):**

```bash
cp ok-init.md ~/.config/opencode/skills/
```

**Local (un solo proyecto):**

```bash
mkdir -p .opencode/skills
cp ok-init.md .opencode/skills/
```
