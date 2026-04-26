# AGENTS.md — {nombre_proyecto}

## Producto

{breve descripción del producto, su propósito y principales características}

## Entorno

### Configuración

- **Carpeta_Raíz**: `/`
- **Carpeta_Agentes**: `/.agents` | `/.claude` | `/.github`
- **Archivo_Agentes**: `/AGENTS.md` | `/CLAUDE.md` | `/.github/copilot-instructions.md`
- **Carpeta_Proyecto**: `/project` | `/docs`
- **SO_dev**: `Windows` | `Linux` | `MacOS`
- **Terminal**: `PowerShell` | `Git Bash` | `Terminal`
- **Rama_por_defecto**: `main` | `master` | `trunk`
- **Git_remote**: {URL del repositorio remoto de git}

### Comportamiento

- Al usar plantillas, reemplaza {placeholders} con valores concretos.
- El código y la documentación deben estar en {idioma_documentacion}.
- Las respuestas del chat deben estar en el idioma del mensaje del usuario.
- Sacrifica la gramática por la concisión cuando sea necesario para ajustarse a los límites de respuesta.
- Siempre realiza linting con `npm run lint` antes de preparar y confirmar cambios.

### Convenciones

Usa slugs con guiones para cualquier identificador: `agregar-tarea`, `corregir-bug`, `actualizar-dependencias`.

## Tecnología

### Stack

- **Lenguaje**: {Lenguaje(s) de programación utilizado(s) en el proyecto}
- **Framework**: {Framework(s) utilizado(s) en el proyecto}
- **Base de datos**: {Base(s) de datos utilizada(s) en el proyecto}
- **Seguridad**: {Configuración de seguridad}
- **Pruebas**: {Frameworks de pruebas}
- **Registro**: {Configuración de registro}

### Flujo de trabajo

```bash
# Configurar el proyecto
{comandos_de_setup}

# Mientras se desarrolla, observa los cambios y ejecuta las pruebas automáticamente
# Observa y compila el proyecto mientras se desarrolla
{comandos_de_watch_y_build}
# Observa y ejecuta pruebas unitarias mientras se escriben pruebas
{comandos_de_watch_de_tests_unitarios}
# Linting estático y verificación de tipos después de escribir código
{comandos_de_lint_y_typecheck}

# Ejecutar pruebas unitarias
{comandos_de_tests_unitarios}
# Ejecutar pruebas end-to-end
{comandos_de_tests_e2e}

# Ejecutar todas las pruebas antes de fusionar o publicar
{comandos_de_todos_los_tests}

# Compilar el proyecto para producción
{comandos_de_build_de_produccion}
# Ejecutar el proyecto como un servidor de producción
{comandos_de_run_de_produccion}
```

### TreeView

```text
.                         # Raíz del proyecto
├── {agents_file}         # Este archivo contiene instrucciones para los agentes
├── README.md             # Descripción general del proyecto
├── {agents_folder}/      # Habilidades y prompts de los agentes
│   └── skills/           # Habilidades de los agentes para tareas específicas
├── {project_folder}/     # Documentación específica del proyecto
│   ├── ADR.md            # Registros de decisiones de arquitectura
│   ├── PRD.md            # Documento de requisitos del producto
│   └── specs/            # Especificaciones del proyecto
├── src/                  # Código fuente de la aplicación
└── other/                # Cualquier otra carpeta o archivo relevante
```

---

> Fin del AGENTS.md · {nombre_proyecto} · {fecha}
