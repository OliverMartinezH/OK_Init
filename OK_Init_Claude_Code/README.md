# OK_Init — Project Governance Skill (Claude Code)

> **For [Claude Code](https://claude.ai/code)** — Generate a complete governance system for any project with Obsidian wiki-links and a KISS workflow protocol.

[![Obsidian](https://img.shields.io/badge/Obsidian-ready-7C3AED?style=flat-square&logo=obsidian)](https://obsidian.md)
[![Claude Code](https://img.shields.io/badge/Claude_Code-000000?style=flat-square)](https://claude.ai/code)
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

## Why OK_Init?

OK_Init is a tool that automatically creates an "intelligence center" for any project. It generates 5 living documents that connect to each other (like Wikipedia) so that the entire team and AI agents always know what is being built, what is missing, and what decisions were made in the past. It's like having a ship's log that writes itself.

### The 5 Commands

| Command | What it does |
|---------|--------------|
| `ok init` | **The starter:** Asks basic questions and sets up the entire structure in seconds |
| `ok sigamos` | **The reminder:** "Where did we leave off?" — reads files and tells you the next step |
| `ok sync` | **The auditor:** Compares real work against the plan and flags incomplete items |
| `ok status` | **The dashboard:** Shows a visual progress bar of where the project stands |
| `ok commit` | **The safe keeper:** Asks quick questions and archives both code and governance notes |

### 3 Business Benefits

| Benefit | Description |
|---------|-------------|
| **No more forgetting** | Leave a project for a month, come back — the tool tells you exactly where you stopped |
| **AI-ready** | If you use AI to work, these files give it perfect context so it doesn't make mistakes |
| **Total independence** | Mobile app, web app, internal system — works exactly the same way |

---

## Installation

### 1. Copy CLAUDE.md

Copy `CLAUDE.md` to your project root.

### 2. Copy skill directory

```bash
mkdir -p .claude/skills/ok-init
cp -r ok-init/* .claude/skills/ok-init/
```

### 3. Verify structure

```
your-project/
├── CLAUDE.md
├── .claude/
│   └── skills/
│       └── ok-init/
│           └── SKILL.md
└── src/
```

---

## Usage

Type any of these commands in Claude Code:

| Command | Action |
|---------|--------|
| `ok init` | Detect files → continue or generate |
| `ok sigamos` | Same as `ok init` |
| `ok sync` | Audit MD vs actual code |
| `ok status` | Show project status dashboard |
| `ok commit` | Commit governance + code (with questions) |

---

## Complete Example

### First time (new project)

1. Open Claude Code in your project folder
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
├── CLAUDE.md
├── .claude/
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

## Requirements

- [Claude Code](https://claude.ai/code) installed
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

## ¿Por qué OK_Init?

OK_Init es una herramienta que crea automáticamente una "central de inteligencia" para cualquier proyecto. Genera 5 documentos vivos que se conectan entre sí (como Wikipedia) para que todo el equipo y las Inteligencias Artificiales sepan siempre qué se está construyendo, qué falta por hacer y qué decisiones se tomaron en el pasado. Es como tener un diario de a bordo que se escribe casi solo.

### Los 5 Comandos

| Comando | Qué hace |
|---------|----------|
| `ok init` | **El arranque:** Hace unas preguntas básicas y monta toda la estructura en un segundo |
| `ok sigamos` | **El recordatorio:** "¿En qué nos quedamos?" — Lee los archivos y te recuerda el siguiente paso |
| `ok sync` | **La auditoría:** Revisa el trabajo real y lo compara con el plan para avisar si algo quedó a medias |
| `ok status` | **El tablero:** Te muestra una barra de progreso visual de cómo va el proyecto hoy |
| `ok commit` | **El archivador seguro:** Te hace preguntas rápidas y archiva tanto los avances como las notas de control |

### Los 3 Grandes Beneficios para el Negocio

| Beneficio | Descripción |
|-----------|-------------|
| **Adiós al olvido** | Si dejas el proyecto un mes y vuelves, la herramienta te dice exactamente dónde te quedaste |
| **Luz para la IA** | Si usas Inteligencia Artificial para trabajar, estos archivos le dan el contexto perfecto para que no cometa errores |
| **Independencia total** | No importa si el proyecto es una aplicación móvil, una web o un sistema interno; funciona exactamente igual |

---

## Instalación

### 1. Copiar CLAUDE.md

Copia `CLAUDE.md` a la raíz de tu proyecto.

### 2. Copiar directorio del skill

```bash
mkdir -p .claude/skills/ok-init
cp -r ok-init/* .claude/skills/ok-init/
```

### 3. Verificar estructura

```
tu-proyecto/
├── CLAUDE.md
├── .claude/
│   └── skills/
│       └── ok-init/
│           └── SKILL.md
└── src/
```

---

## Uso

Escribe cualquiera de estos comandos en Claude Code:

| Comando | Acción |
|---------|--------|
| `ok init` | Detectar archivos → continuar o generar |
| `ok sigamos` | Igual que `ok init` |
| `ok sync` | Auditar MD vs código real |
| `ok status` | Mostrar dashboard del estado del arte |
| `ok commit` | Commitear governance + código (con preguntas) |

---

## Ejemplo Completo

### Primera vez (proyecto nuevo)

1. Abrir Claude Code en la carpeta del proyecto
2. Escribir: `ok init`
3. Responder 6 preguntas (o Enter para valores por defecto)
4. ¡Se generan los archivos!
5. Empezar a codificar con la IA

### Durante una sesión

1. Escribir: `ok sigamos` (para continuar)
2. Trabajar en el paso actual
3. Cuando termines: `ok sync` (para auditar)
4. Cuando estés listo: `ok commit` (para guardar)

---

## Diagrama de Flujo

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

## Requisitos

- [Claude Code](https://claude.ai/code) instalado
- Obsidian (opcional, para graph views)

---

## Licencia

MIT
