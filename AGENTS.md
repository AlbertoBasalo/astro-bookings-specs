# Instrucciones

## Producto

**AstroBookings** es un sistema de reserva de vuelos espaciales utilizado como demostración en cursos de formación.

## Entorno

### Configuración

- **Root_Folder**: `/`
- **Agents_Folder**: `/.agents`
- **Agents_file**: `/AGENTS.md`
- **Project_Folder**: `/project`
- **OS dev**: `Windows` 
- **Terminal**: `PowerShell` 
- **Git remote**: `https://github.com/AlbertoBasalo/astro-bookings-specs.git`
- **Default branch**: `main`

### Comportamiento

- Las respuestas del chat deben estar en el idioma del prompt del usuario.
- Sacrificar gramática para mayor concisión y reducir el tamaño de las respuestas.
- Cuando se utilicen plantillas, reemplaza los {placeholders} con valores concretos.
- El código y la documentación deben estar en español.
- Puedes mezclar con ingles en términos técnicos o de programación (`get`, `can`, `has`, `etc.`).

### Convenciones

Utiliza slugs con guiones para cualquier identificador: `add-tarea`, `fix-fallo-en-login`, `update-dependencias`.

## Tecnología

### Stack

- **Language**: No determinado por ahora.
- **Framework**: No determinado por ahora.
- **Database**: No determinado por ahora.
- **Security**: No determinado por ahora.
- **Testing**: No determinado por ahora.
- **Logging**: No determinado por ahora.

### Flujo de trabajo para el desarrollo

```bash
# Set up del proyecto
No determinado por ahora.

# Mientras desarrollamos, observamos cambios y ejecutamos tests automáticamente
No determinado por ahora.

# Compilar el proyecto para producción
No determinado por ahora.

# Ejecutar el proyecto como servidor de producción
No determinado por ahora.
```

### Vista en árbol

```text
.                         # Carpeta raíz del proyecto
├── {agents_file}         # Este archivo con las instrucciones para los agentes
├── README.md             # Resumen del proyecto
├── {agents_folder}/      # Configuración de los agentes
│   └── skills/           # Habilidades para tareas específicas
├── {project_folder}/     # Documentación específica del proyecto
│   ├── PRD.md            # Documento de Requerimientos de Producto
│   └── specs/            # Especificaciones funcionales del proyecto
└── otros/                # Otras carpetas o archivos relevantes
```

