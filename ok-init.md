# OK_Init — Skill de Inicialización de Proyecto con Gobernanza

**Nombre:** ok-init
**Trigger:** "iniciar proyecto", "OK_Init", "crear gobernanza", "ok init"
**Descripción:** Genera el sistema de gobernanza de 6 archivos MD para un proyecto .NET con Arquitectura Hexagonal, incluyendo enlaces Obsidian bidireccionales.

---

## Instrucciones para la IA

Cuando el usuario active esta skill, debes:

### Paso 1: Recopilar datos (9 preguntas)

Haz las siguientes preguntas **una por una** o **en grupo** (máximo 3 por mensaje para no abrumar):

| # | Pregunta | Placeholder | Ejemplo |
|---|----------|-------------|---------|
| 1 | ¿Cuál es el nombre del proyecto? | `{{PROJECT_NAME}}` | OKSoft |
| 2 | ¿Cuál es el nombre del módulo central/Kernel? | `{{KERNEL_NAME}}` | OKKernel |
| 3 | ¿Cuáles son los módulos de negocio? (separados por coma) | `{{MODULES}}` | OKPersonal, OKInventario |
| 4 | ¿Qué stack tecnológico usas? | `{{STACK}}` | .NET 10 + C# 14 |
| 5 | ¿Qué base de datos usas? | `{{DATABASE}}` | SQL Server 2022 |
| 6 | ¿Qué framework de testing usas? | `{{TEST_FRAMEWORK}}` | xUnit + Moq |
| 7 | ¿Qué framework UI/CSS usas? | `{{UI_FRAMEWORK}}` | Tailwind CDN |
| 8 | ¿Qué estrategia de autenticación usas? | `{{AUTH_STRATEGY}}` | Cookie Authentication |
| 9 | ¿Cuáles son los esquemas de DB por módulo? (formato: kernel=esquema, modulo=esquema) | `{{DB_SCHEMAS}}` | oliver=oliver, OKPersonal=personal, OKInventario=inventario |

### Paso 2: Generar los 6 archivos

Genera los siguientes archivos en el directorio de trabajo actual:

#### Archivo 1: `Proyecto {{PROJECT_NAME}}.md`

```markdown
# Mapa del Proyecto: Ecosistema {{PROJECT_NAME}}

> **Contexto técnico:** Ver [[stack]]
> **Reglas de desarrollo:** Ver [[agent]]
> **Estado de avance:** Ver [[progress]]

---

## Filosofía de Desarrollo

* **Gobernanza desde el Kernel:** Ningún módulo decide de forma autónoma si está disponible o no. Todo se valida consultando la infraestructura de `{{KERNEL_NAME}}`.
* **Simplicidad Extrema (KISS):** Evita la sobre-ingeniería.
* **Gestión de Errores:** Utiliza exclusivamente la estructura `Result` o `Result<T>` para notificar fallos lógicos.
* **Autenticación:** {{AUTH_STRATEGY}}.
* **Control de Acceso:** Filtro guardián que verifica activación del módulo + permiso del rol.

---

## Arquitectura y Componentes

### Capa Core e Infraestructura Central
* **Control Global:** `{{PROJECT_NAME}}.{{KERNEL_NAME}}.Core` — Contenedor del patrón `Result`.
* **Base de Datos Principal:** `{{PROJECT_NAME}}.{{KERNEL_NAME}}.Infrastructure` — DbContext central y filtro guardián.
* **Panel de Control:** `{{PROJECT_NAME}}.{{KERNEL_NAME}}.AdminUI` — Panel administrativo.

{{#each MODULES}}
### Módulo: {{this}}
* **Dominio:** `{{PROJECT_NAME}}.{{this}}.Domain` — Entidades y puertos.
* **Aplicación:** `{{PROJECT_NAME}}.{{this}}.Application` — Casos de uso.
* **Infraestructura:** `{{PROJECT_NAME}}.{{this}}.Infrastructure` — DbContext y repositorios.
* **Presentación:** `{{PROJECT_NAME}}.{{this}}.Presentation` — Controladores y vistas.
{{/each}}

### Calidad y Pruebas
* **Pruebas:** `tests/{{PROJECT_NAME}}.Tests` — Pruebas unitarias en **{{TEST_FRAMEWORK}}**.

---

## Hoja de Ruta

1. Infraestructura base del Kernel
{{#each MODULES}}
{{@index}}. Módulo {{this}}
{{/each}}
{{@last}}. Ensamblaje final
```

#### Archivo 2: `agent.md`

```markdown
# Agent Instructions: Generación de Código Ecosistema {{PROJECT_NAME}}

> **Mapa del proyecto:** Ver [[Proyecto {{PROJECT_NAME}}]]
> **Stack tecnológico:** Ver [[stack]]
> **Estado actual:** Ver [[progress]]
> **Historial de fases:** Ver [[history]]

---

## 1. Filosofía de Desarrollo Obligatoria

* **Gobernanza desde el Kernel:** Ningún módulo decide de forma autónoma si está disponible o no. Todo se valida consultando la infraestructura de `{{KERNEL_NAME}}`.
* **Simplicidad Extrema (KISS):** Evita la sobre-ingeniería.
* **Gestión de Errores:** No uses excepciones para controlar validaciones de negocio. Utiliza exclusivamente la estructura `Result` o `Result<T>`.
* **Autenticación:** {{AUTH_STRATEGY}}.
* **Control de Acceso:** Filtro guardián que verifica:
  1. ¿El módulo está activo en DB?
  2. ¿El rol del usuario autenticado tiene acceso al módulo?

---

## 2. Directrices de Testing

* Cada proyecto en `src/` tiene su espejo de tests en `tests/` con el sufijo `.Tests`.
* Framework: **{{TEST_FRAMEWORK}}**.
* Nombre de métodos: `[Método]_[Escenario]_[ResultadoEsperado]`.
* Todo el código nuevo DEBE tener tests unitarios antes de darse por completado.

---

## 3. Hoja de Ruta para la Generación de Código

### Paso 1: Infraestructura Base de {{KERNEL_NAME}}
1. **Core:** Crear la clase contenedora del patrón `Result`.
2. **Infrastructure:** Crear el `DbContext` asignado al esquema correspondiente.
3. **Filtro Guardián:** Crear un `ActionFilterAttribute` global para control de acceso.
4. **AdminUI:** Crear el proyecto Razor Class Library con el panel administrativo.
5. **Menú Dinámico:** ViewComponent de navegación.

{{#each MODULES}}
### Paso {{@index + 2}}: Desarrollo del Módulo {{this}}
1. **Domain:** Generar las entidades correspondientes en 3NF.
2. **Application:** Escribir los casos de uso con patrón `Result`.
3. **Infrastructure:** Configurar el `DbContext` del módulo.
4. **Presentation:** Desarrollar controlador y vistas.
{{/each}}

---

## 4. Decisiones y Reglas Acordadas

> [!note] Historial de sesiones
> Este espacio se llena automáticamente durante el desarrollo.
> Las decisiones acordadas se registran aquí para referencia futura.

* Pendiente de primera sesión de desarrollo.
```

#### Archivo 3: `stack.md`

```markdown
# Tech Stack & Architectural Blueprint: {{PROJECT_NAME}} Monolith

> **Mapa del proyecto:** Ver [[Proyecto {{PROJECT_NAME}}]]
> **Reglas de código:** Ver [[agent]]
> **Estado actual:** Ver [[progress]]

---

## 1. Tecnologías Centrales

* **Runtime:** {{STACK}}
* **Enfoque:** Monolito Modular Limpio bajo el principio KISS.
* **Estilo Arquitectónico:** Arquitectura Hexagonal (Ports & Adapters) por cada módulo.
* **Framework Web:** ASP.NET Core MVC con Vistas Razor.
* **Acceso a Datos:** Entity Framework Core (Code-First) con un DbContext por módulo.
* **Base de Datos:** {{DATABASE}} con aislamiento por esquemas.
* **Autenticación:** {{AUTH_STRATEGY}}.
* **Testing:** {{TEST_FRAMEWORK}}.
* **UI:** {{UI_FRAMEWORK}}.

---

## 2. Gobernanza Central: {{KERNEL_NAME}}

* **Control de Estado:** Tabla centralizada que define si un módulo está activo.
* **Control de Acceso:** Roles por módulo.
* **Gobernanza de Acceso (KISS):** Filtro `ActionFilter` global.
* **UI Dinámica:** Barra de navegación que consulta al Kernel.

---

## 3. Modelo de Datos (3NF Estricta)

> [!important] Esquemas por módulo
> Cada módulo tiene su propio esquema en la misma base de datos.

### Esquemas
{{#each DB_SCHEMAS}}
* **`{{this}}`** — Módulo {{@key}}
{{/each}}

> [!tip] Diseño de datos
> Organiza las entidades en esquemas independientes para facilitar el aislamiento.

---

## 4. Estructura de la Solución

```text
{{PROJECT_NAME}}/
├── src/
│   ├── BuildingBlocks/
│   │   └── {{KERNEL_NAME}}/
│   │       ├── {{PROJECT_NAME}}.{{KERNEL_NAME}}.Core/
│   │       ├── {{PROJECT_NAME}}.{{KERNEL_NAME}}.Infrastructure/
│   │       └── {{PROJECT_NAME}}.{{KERNEL_NAME}}.AdminUI/
│   ├── Modules/
{{#each MODULES}}
│   │   ├── {{this}}/
│   │   │   ├── {{PROJECT_NAME}}.{{this}}.Domain/
│   │   │   ├── {{PROJECT_NAME}}.{{this}}.Application/
│   │   │   ├── {{PROJECT_NAME}}.{{this}}.Infrastructure/
│   │   │   └── {{PROJECT_NAME}}.{{this}}.Presentation/
{{/each}}
│   └── Web/
│       └── {{PROJECT_NAME}}.WebHost/
```

---

## 5. Estructura de Tests

```text
{{PROJECT_NAME}}/
└── tests/
    └── BuildingBlocks/
        └── {{KERNEL_NAME}}/
            ├── {{PROJECT_NAME}}.{{KERNEL_NAME}}.Core.Tests/
            ├── {{PROJECT_NAME}}.{{KERNEL_NAME}}.Infrastructure.Tests/
            └── {{PROJECT_NAME}}.{{KERNEL_NAME}}.AdminUI.Tests/
```

---

## 6. Estándar de Interfaz Visual

> [!note] Estándar UI
> Toda la interfaz web debe heredar un diseño moderno, minimalista y de alta gama.

* **Engine UI (KISS):** {{UI_FRAMEWORK}} cargado vía CDN.
* **Línea Gráfica Corporativa:**
  * Fondo Base: Blanco puro y gris ultra claro.
  * Color Primario: Indigo Tecnológico.
  * Paleta de Estados: Verde (habilitados), Ámbar (alertas), Rojo (errores).
* **Componentes UI:**
  * Layout SaaS Dashboard con barra lateral fija.
  * Tablas con bordes redondeados y sombras sutiles.
  * Formularios con etiquetas pequeñas y esquinas suavizadas.
  * Botones con transiciones suaves.

---

## 7. Docker

```yaml
version: '3.8'

services:
  sqlserver:
    image: mcr.microsoft.com/mssql/server:2022-latest
    container_name: {{PROJECT_NAME, lowercase}}_sqlserver
    environment:
      - ACCEPT_EULA=Y
      - MSSQL_SA_PASSWORD=YourSecurePassword123!
    ports:
      - "1433:1433"
    volumes:
      - {{PROJECT_NAME, lowercase}}_data:/var/opt/mssql

  webhost:
    image: {{PROJECT_NAME, lowercase}}-webhost:latest
    build:
      context: .
      dockerfile: src/Web/{{PROJECT_NAME}}.WebHost/Dockerfile
    ports:
      - "8080:80"
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
    depends_on:
      - sqlserver

volumes:
  {{PROJECT_NAME, lowercase}}_data:
```
```

#### Archivo 4: `progress.md`

```markdown
# {{PROJECT_NAME}} - Bitácora de Progreso

> **Historial de fases:** Ver [[history]]
> **Stack tecnológico:** Ver [[stack]]
> **Reglas de código:** Ver [[agent]]
> **Mapa del proyecto:** Ver [[Proyecto {{PROJECT_NAME}}]]

---

## 1. Estado General del Proyecto

* **Proyecto:** {{PROJECT_NAME}} ({{STACK}} + Arquitectura Hexagonal)
* **Fase Actual:** Pendiente de inicio
* **Último hito completado:** Ninguno

---

## 2. Checklist de Implementación

### Fase 0: Infraestructura de Testing
- [ ] **0.1.** Crear proyecto de tests con {{TEST_FRAMEWORK}}
- [ ] **0.2.** Tests del patrón Result
- [ ] **0.3.** Tests de infraestructura

### Fase 1: El Exoesqueleto ({{KERNEL_NAME}})
- [ ] **1.1.** Crear clase `Result<T>`
- [ ] **1.2.** Crear `DbContext` central
- [ ] **1.3.** Crear filtro guardián
- [ ] **1.4.** Crear panel administrativo
- [ ] **1.5.** Crear menú dinámico

{{#each MODULES}}
### Fase {{@index + 2}}: Módulo {{this}}
- [ ] **{{@index + 2}}.1.** Dominio (3NF)
- [ ] **{{@index + 2}}.2.** Aplicación (Casos de uso)
- [ ] **{{@index + 2}}.3.** Infraestructura (DbContext + Repositorios)
- [ ] **{{@index + 2}}.4.** Presentación (Controlador + Vistas)
{{/each}}

---

## 3. Bitácora de Iteraciones Recientes

* Pendiente de primera iteración.

---

## 4. Próximo Paso Inmediato

> [!tip] Primer paso
> Comienza con la Fase 0: Infraestructura de Testing.
```

#### Archivo 5: `history.md`

```markdown
# {{PROJECT_NAME}} — Historial de Fases Completadas

> **Estado actual:** Ver [[progress]]
> **Stack tecnológico:** Ver [[stack]]
> **Reglas de código:** Ver [[agent]]

---

> [!note] Archivo acumulativo
> Este archivo registra todas las fases completadas con fecha y hora.
> Se actualiza automáticamente cuando se completa una fase en [[progress]].

---

*No hay fases completadas aún.*
```

#### Archivo 6: `prompt.txt`

```text
Hola, vamos a comenzar a trabajar en el proyecto {{PROJECT_NAME}}.
Te adjunto stack.md, agent.md y progress.md para que sepas en qué vamos.
Recuerda usar el MCP context7.

Por favor, lee el 'Próximo Paso Inmediato' del progress.md y genérame el código correspondiente.

---

REGLA DE GOBERNANZA OBLIGATORIA (KISS)

1. ANTES DE CODIFICAR: Lee el 'Próximo Paso Inmediato' del progress.md. Si algo es ambiguo, consúltame antes de escribir código.

2. SCOPE ESTRICTO: Genera únicamente el código para ese archivo específico.

3. DEPENDENCIAS MENORES: Si el archivo requiere un tipo que aún no existe, crea un stub con comentario // TODO.

4. FORMATO DE ENTREGA: Ruta completa del archivo como encabezado.

5. DETENTE Y ESPERA APROBACIÓN: Al terminar, preséntame un resumen y espera mi aprobación.

6. CIERRE DE ETAPA (solo tras aprobación):
   - progress.md → marca completado y establece próximo paso.
   - history.md → mueve la etapa completada con fecha.
   - stack.md → documenta decisiones técnicas.
   - agent.md → documenta reglas nuevas.
```

### Paso 3: Crear `.opencode.json`

Si no existe, crear `opencode.json` en el directorio actual:

```json
{
  "$schema": "https://opencode.ai",
  "mcp": {
    "microsoft-docs": {
      "type": "remote",
      "url": "https://learn.microsoft.com/api/mcp",
      "enabled": true
    }
  }
}
```

### Paso 4: Preguntar sobre copia global

Preguntar al usuario:
> ¿Quieres copiar la skill a `~/.config/opencode/skills/` para que esté disponible en todos los proyectos?

Si responde sí, copiar `ok-init.md` a `%USERPROFILE%\.config\opencode\skills\ok-init.md`.

### Paso 5: Confirmar

Mostrar resumen de archivos creados y preguntar si quiere abrir Obsidian para verificar los links.

---

## Notas de Implementación

### Reemplazos dinámicos

| Variable | Descripción | Ejemplo |
|----------|-------------|---------|
| `{{PROJECT_NAME}}` | Nombre del proyecto | OKSoft |
| `{{KERNEL_NAME}}` | Nombre del módulo central | OKKernel |
| `{{MODULES}}` | Lista de módulos | OKPersonal, OKInventario |
| `{{STACK}}` | Stack tecnológico | .NET 10 + C# 14 |
| `{{DATABASE}}` | Base de datos | SQL Server 2022 |
| `{{TEST_FRAMEWORK}}` | Framework de testing | xUnit + Moq |
| `{{UI_FRAMEWORK}}` | Framework UI | Tailwind CDN |
| `{{AUTH_STRATEGY}}` | Estrategia de auth | Cookie Authentication |
| `{{DB_SCHEMAS}}` | Esquemas por módulo | oliver=oliver, OKPersonal=personal |

### Formato de fechas

Usar formato: `DD/MM/YYYY HH:MM` con zona horaria `America/Santiago`.

### Obsidian Features

- **Wiki-links:** `[[archivo]]` entre los 5 archivos MD
- **Callouts:** `> [!note]`, `> [!tip]`, `> [!warning]`, `> [!important]`
- **Tags:** `#fase/0`, `#fase/1`, `#modulo/{{MODULE_NAME}}`
- **Graph view:** Se genera automáticamente por los wiki-links

### Validación

Antes de confirmar la creación:
1. Verificar que no existen archivos con el mismo nombre (preguntar si sobreescribir)
2. Validar que las rutas son accesibles
3. Confirmar que Obsidian puede leer los archivos (formato UTF-8)
