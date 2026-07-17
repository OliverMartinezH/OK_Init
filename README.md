# OK_Init — Project Governance Skill

> **For [opencode](https://opencode.ai)** — Generate a complete governance system for any project with Obsidian wiki-links and a KISS workflow protocol.

[![Obsidian](https://img.shields.io/badge/Obsidian-ready-7C3AED?style=flat-square&logo=obsidian)](https://obsidian.md)
[![opencode](https://img.shields.io/badge/opencode-000000?style=flat-square)](https://opencode.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)
[![OpenCode](https://img.shields.io/badge/opencode-000000?style=flat-square)](https://opencode.ai)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-D97757?style=flat-square&logo=claudecode&logoColor=white)](https://claude.com)
[![Antigravity](https://img.shields.io/badge/Antigravity-4285F4?style=flat-square&logo=google&logoColor=white)](https://antigravity.google)
[![Cursor](https://img.shields.io/badge/Cursor-000000?style=flat-square&logo=cursor&logoColor=white)](https://cursor.com)
[![Windsurf](https://img.shields.io/badge/Windsurf-00A6FF?style=flat-square&logo=windsurf&logoColor=white)](https://windsurf.com)
[![Cline](https://img.shields.io/badge/Cline-E8593C?style=flat-square&logo=cline&logoColor=white)](https://cline.bot)
[![Aider](https://img.shields.io/badge/Aider-6B4FBB?style=flat-square)](https://aider.chat)

---

## What is OK_Init?

> **OK_Init is a file-based "long-term memory" for free AI tools (ChatGPT, Claude, opencode).**
> It saves you time and money (tokens).
>
> Free AI tiers forget your project context quickly — leading to mistakes, repeated explanations, or starting from scratch. OK_Init creates 5 interconnected text files that summarize your project perfectly. Each time you start a session, you paste one of these files into the AI: it understands everything instantly, uses the minimum data possible, and guides you step by step to finish tasks without going in circles.

### The 3 Pillars of Savings

| Pillar | Analogy | What it does |
|--------|---------|--------------|
| 💾 **External memory for AI** | Like giving it a memory card with the exact summary | Instead of explaining your project in every message, just pass `agent.md` or `progress.md` |
| 🎯 **Zero runaround (fewer messages)** | Solve in 2 messages instead of 10 | `ok sigamos` tells you the exact next step, avoiding daily free-tier message limits |
| 🔍 **Garbage filter** | Skip what's already done | `ok sync` detects what's built and what's not — no wasted tokens reviewing ready code |

#### How it works

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

## The 5 Commands

| Command | What it does |
|---------|--------------|
| `ok init` | **The starter:** Asks basic questions and sets up the entire structure in seconds |
| `ok sigamos` | **The reminder:** "Where did we leave off?" — reads files and tells you the next step |
| `ok sync` | **The auditor:** Compares real work against the plan and flags incomplete items |
| `ok status` | **The dashboard:** Shows a visual progress bar of where the project stands |
| `ok commit` | **The safe keeper:** Asks quick questions and archives both code and governance notes |

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
# Copy skill directory to global skills directory
mkdir -p ~/.config/opencode/skills/ok-init
cp .opencode/skills/ok-init/SKILL.md ~/.config/opencode/skills/ok-init/
```

**Local (single project):**

```bash
# Copy skill directory to your project's .opencode directory
mkdir -p .opencode/skills/ok-init
cp .opencode/skills/ok-init/SKILL.md .opencode/skills/ok-init/
```

> [!important] Correct structure
> Skills MUST follow the `.opencode/skills/<name>/SKILL.md` format with proper frontmatter. The `name` field in frontmatter must match the folder name.

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

> [!warning] Privacy notice
> This mode reads the current conversation to extract project decisions only. Avoid sharing sensitive data (API keys, passwords, personal info) in the chat before using this mode.

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

## Complete Example

### First time (new project)

1. Open opencode in your project folder
2. Type: `ok init`
3. Answer 6 questions (or press Enter for defaults)
4. Files are generated!
5. Start coding with the AI

### During a session

1. Type: `ok sigamos` (to continue)
2. Work on the current step
3. When done: `ok sync` (to audit)
4. When ready: `ok commit` (to save)

### Flowchart

```
┌─────────────────────────────────────────────────────────────┐
│                      OK_Init Workflow                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐              │
│  │ ok init  │───▶│ 6 Q's    │───▶│ 5 files  │              │
│  └──────────┘    └──────────┘    └──────────┘              │
│       │                              │                      │
│       ▼                              ▼                      │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐              │
│  │ok sigamos│───▶│  Read    │───▶│  Work    │              │
│  └──────────┘    │  state   │    │  on code │              │
│                  └──────────┘    └──────────┘              │
│                                     │                       │
│                                     ▼                       │
│                              ┌──────────┐                   │
│                              │ ok sync  │                   │
│                              └──────────┘                   │
│                                     │                       │
│                                     ▼                       │
│                              ┌──────────┐                   │
│                              │ok commit │                   │
│                              └──────────┘                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
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
├── .opencode/
│   └── skills/
│       └── ok-init/
│           └── SKILL.md
├── Proyecto [YOUR_PROJECT].md
├── agent.md
├── stack.md
├── progress.md
└── history.md
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

## Agentes Compatibles

OK_Init es compatible de forma nativa con los principales agentes CLI del ecosistema. Al instalar el skill, el agente solo consumirá tokens cuando invoques los comandos, manteniendo tu contexto limpio.

| Plataforma | Tipo | Instalación |
|------------|------|-------------|
| **OpenCode** | Skill (SKILL.md) | `cp ok-init.md ~/.config/opencode/skills/` |
| **Claude Code** | Skill (SKILL.md) | `mkdir -p .claude/skills/ok-init && cp SKILL.md .claude/skills/ok-init/` |
| **Antigravity** | Skill (SKILL.md) | `mkdir -p .agent/skills/ok-init && cp SKILL.md .agent/skills/ok-init/` |
| **Cursor** | Rules (.cursorrules) | `cp .cursorrules .cursorrules` |
| **Windsurf** | Rules (.windsurfrules) | `cp .windsurfrules .windsurfrules` |
| **Cline** | Rules (.clinerules/) | `mkdir -p .clinerules && cp .clinerules/governance.md .clinerules/` |
| **Aider** | Conventions (CONVENTIONS.md) | `cp CONVENTIONS.md .` |

### Instalación por Plataforma

#### 1. OpenCode
```bash
cp ok-init.md ~/.config/opencode/skills/
```

#### 2. Claude Code
```bash
mkdir -p .claude/skills/ok-init
cp SKILL.md .claude/skills/ok-init/
```

#### 3. Google Antigravity
```bash
mkdir -p .agent/skills/ok-init
cp SKILL.md .agent/skills/ok-init/
```

#### 4. Cursor / Windsurf
```bash
# Cursor
cp .cursorrules .cursorrules

# Windsurf
cp .windsurfrules .windsurfrules
```

#### 5. Cline
```bash
mkdir -p .clinerules
cp .clinerules/governance.md .clinerules/
```

#### 6. Aider
```bash
cp CONVENTIONS.md .
```

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

## ¿Por qué OK_Init?

> **OK_Init es un sistema de archivos inteligentes que le da "memoria a largo plazo" a las Inteligencias Artificiales gratuitas (como ChatGPT o Claude).**
> Su objetivo es ahorrarte tiempo y dinero (tokens).
>
> En las versiones gratis, la IA olvida el contexto rápidamente y empieza a cometer errores o te obliga a reescribir todo desde el principio. OK_Init crea 5 notas de texto interconectadas que resumen perfectamente tu proyecto. Cada vez que inicias una sesión, le pegas una de estas notas a la IA: así ella entiende todo al instante, consume el mínimo de datos posible y te guía paso a paso para terminar tareas sin dar vueltas en círculo.

### Los 3 Pilares del Ahorro

| Pilar | Analogía | Qué hace |
|-------|----------|----------|
| 💾 **Memoria externa para la IA** | Como darle una tarjeta de memoria con el resumen exacto | En lugar de gastar espacio explicándole tu proyecto en cada mensaje, solo le pasas `agent.md` o `progress.md` |
| 🎯 **Cero rodeos (menos mensajes)** | Resuelves en 2 mensajes en lugar de 10 | `ok sigamos` te dice el siguiente paso exacto, evitando que se agote tu límite diario de la versión gratuita |
| 🔍 **Filtro de basura** | No gastas tokens revisando código que ya estaba listo | `ok sync` detecta qué se programó y qué no, para no analizar archivos irrelevantes |

### Los 5 Comandos

| Comando | Qué hace |
|---------|----------|
| `ok init` | **El arranque:** Hace unas preguntas básicas y monta toda la estructura en un segundo |
| `ok sigamos` | **El recordatorio:** "¿En qué nos quedamos?" — Lee los archivos y te recuerda el siguiente paso |
| `ok sync` | **La auditoría:** Revisa el trabajo real y lo compara con el plan para avisar si algo quedó a medias |
| `ok status` | **El tablero:** Te muestra una barra de progreso visual de cómo va el proyecto hoy |
| `ok commit` | **El archivador seguro:** Te hace preguntas rápidas y archiva tanto los avances como las notas de control |

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

## Ejemplo Completo

### Primera vez (proyecto nuevo)

1. Abrir opencode en la carpeta del proyecto
2. Escribir: `ok init`
3. Responder 6 preguntas (o Enter para valores por defecto)
4. ¡Se generan los archivos!
5. Empezar a codificar con la IA

### Durante una sesión

1. Escribir: `ok sigamos` (para continuar)
2. Trabajar en el paso actual
3. Cuando termines: `ok sync` (para auditar)
4. Cuando estés listo: `ok commit` (para guardar)

### Diagrama de Flujo

```
┌─────────────────────────────────────────────────────────────┐
│                   Flujo de Trabajo OK_Init                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐              │
│  │ ok init  │───▶│ 6 Preg.  │───▶│ 5 archivos│             │
│  └──────────┘    └──────────┘    └──────────┘              │
│       │                              │                      │
│       ▼                              ▼                      │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐              │
│  │ok sigamos│───▶│  Leer    │───▶│ Trabajar │              │
│  └──────────┘    │  estado  │    │  código  │              │
│                  └──────────┘    └──────────┘              │
│                                     │                       │
│                                     ▼                       │
│                              ┌──────────┐                   │
│                              │ ok sync  │                   │
│                              └──────────┘                   │
│                                     │                       │
│                                     ▼                       │
│                              ┌──────────┐                   │
│                              │ok commit │                   │
│                              └──────────┘                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Instalación

**Global (todos los proyectos):**

```bash
mkdir -p ~/.config/opencode/skills/ok-init
cp .opencode/skills/ok-init/SKILL.md ~/.config/opencode/skills/ok-init/
```

**Local (un solo proyecto):**

```bash
mkdir -p .opencode/skills/ok-init
cp .opencode/skills/ok-init/SKILL.md .opencode/skills/ok-init/
```

> [!important] Estructura correcta
> Los skills DEBEN seguir el formato `.opencode/skills/<nombre>/SKILL.md` con frontmatter válido. El campo `name` en el frontmatter debe coincidir con el nombre de la carpeta.
