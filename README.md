# OK_Init — Skill de Inicialización de Proyecto

Skill para [opencode](https://opencode.ai) que genera un sistema de gobernanza completo para proyectos .NET con Arquitectura Hexagonal.

## Qué genera

La skill crea **6 archivos** al iniciar un nuevo proyecto:

| Archivo | Propósito |
|---------|-----------|
| `Proyecto {{NAME}}.md` | Mapa arquitectónico del proyecto |
| `agent.md` | Reglas de código + historial de decisiones |
| `stack.md` | Stack técnico + modelo de datos + estándar UI |
| `progress.md` | Estado actual + próximo paso |
| `history.md` | Memoria acumulativa de fases completadas |
| `prompt.txt` | Protocolo de sesión para cada iteración |

## Características

- **Obsidian-ready:** Todos los archivos MD se enlazan entre sí con `[[wiki-links]]`
- **Callouts:** Incluye `> [!note]`, `> [!tip]`, `> [!warning]`, `> [!important]`
- **Graph view:** Obsidian genera automáticamente el grafo de relaciones
- **9 preguntas personalizables:** Proyecto, Kernel, módulos, stack, DB, testing, UI, auth, esquemas

## Instalación

### Opción 1: Local (solo este proyecto)

Copia `ok-init.md` a `.opencode/skills/` en tu workspace:

```
tu-proyecto/
└── .opencode/
    └── skills/
        └── ok-init.md
```

### Opción 2: Global (todos los proyectos)

Copia `ok-init.md` a `~/.config/opencode/skills/`:

```
~/.config/opencode/skills/
└── ok-init.md
```

## Uso

En opencode, escribe cualquiera de estos comandos:

```
iniciar proyecto
OK_Init
crear gobernanza
ok init
```

La IA te preguntará 9 datos y generará los 6 archivos personalizados.

## Ejemplo de salida

### Graph view en Obsidian

```
┌─────────────┐
│  Proyecto   │
│   OKSoft    │
└──────┬──────┘
       │
       ▼
┌──────────────┐     ┌──────────────┐
│   stack      │◄────│   agent      │
│  (técnico)   │     │  (reglas)    │
└──────┬───────┘     └──────┬───────┘
       │                    │
       ▼                    ▼
┌──────────────┐     ┌──────────────┐
│  progress    │◄────│   history    │
│  (estado)    │     │  (memoria)   │
└──────────────┘     └──────────────┘
```

### Preguntas que hace

1. Nombre del proyecto → `OKSoft`
2. Nombre del Kernel → `OKKernel`
3. Módulos de negocio → `OKPersonal, OKInventario`
4. Stack tecnológico → `.NET 10 + C# 14`
5. Base de datos → `SQL Server 2022`
6. Framework testing → `xUnit + Moq`
7. Framework UI → `Tailwind CDN`
8. Estrategia auth → `Cookie Authentication`
9. Esquemas DB → `oliver=oliver, OKPersonal=personal, OKInventario=inventario`

## Estructura de archivos generados

```
tu-proyecto/
├── Proyecto OKSoft.md
├── agent.md
├── stack.md
├── progress.md
├── history.md
├── prompt.txt
└── opencode.json (si no existía)
```

## Requisitos

- [opencode](https://opencode.ai) instalado
- Obsidian (opcional, para ver los graph views)

## Licencia

MIT
