---
name: refining-skills
description: Estandariza y mejora skills existentes del proyecto, detectando inconsistencias de estructura, redacción y criterios de calidad. Usar cuando se cree una skill nueva o se quiera refinar una colección de SKILL.md para que sean homogéneos.
---

# Refinar y homogeneizar skills

## Rol

Actúa como editor de calidad de Agent Skills.
Tu objetivo es convertir un conjunto de `SKILL.md` en un sistema coherente, fácil de mantener y fácil de descubrir por el agente.

## Tarea

Auditar y normalizar skills del repositorio para que compartan:
- estructura común
- terminología consistente
- reglas de redacción comparables
- checklist de verificación uniforme

Regla crítica:
- No generes un reporte.
- Haz solo los cambios mínimos necesarios.

## Contexto

- Skills de proyecto en `{Agents_Folder}/skills/`
- Reglas globales en `{Root_Folder}/AGENTS.md`
- Opcional: skills de referencia externas (si el usuario las aporta)

## Pasos

### 1) Inventario rápido

Para cada skill objetivo:
- localiza `name` y `description` del frontmatter
- identifica secciones principales del cuerpo
- detecta plantillas o ficheros auxiliares enlazados

Resultado: tabla mental `skill -> estructura -> gaps`.

### 2) Auditoria de homogeneidad

Evalúa cada `SKILL.md` con estos criterios:

- **Frontmatter**
  - `name` en kebab-case y coherente con la carpeta
  - `description` en tercera persona
  - `description` incluye `QUE hace` + `CUANDO usarla`
- **Estructura**
  - usa orden base: `Rol`, `Tarea`, `Contexto` (si aplica), `Pasos`, `Verificacion`
  - títulos en un único idioma (evitar mezcla innecesaria)
- **Redacción**
  - verbos imperativos claros
  - evitar ambigüedad y repeticiones
  - estilo conciso, sin teoría básica
- **Consistencia operativa**
  - rutas y placeholders consistentes (`{Project_Folder}`, `{Root_Folder}`, etc.)
  - nomenclatura uniforme (`Briefing`, `PRD`, `spec`, `FR`, `TR`)
  - reglas de preguntas aclaratorias alineadas entre skills
- **Verificación**
  - checklist accionable (checkboxes)
  - criterio observable, no vago

### 3) Plan de normalización

Clasifica hallazgos por severidad:
- **Critico**: rompe ejecución de la skill o produce salidas ambiguas
- **Importante**: genera inconsistencia entre skills
- **Mejora**: optimiza claridad o mantenibilidad

Propone cambios minimos y concretos por archivo.

### 4) Aplicación de cambios

Cuando el usuario pida editar:
- aplica cambios manteniendo el objetivo funcional original de cada skill
- evita sobre-redisenar: corrige solo lo necesario para converger en estándar común
- preserva enlaces validos a plantillas y documentos relacionados

### 5) Cierre

Al terminar:
- aplica directamente los cambios acordados
- explica el resultado en 2-4 bullets máximo

## Reglas de estilo para skills del proyecto

- Escribir documentación en español (términos técnicos en inglés cuando aporte precisión).
- Mantener `SKILL.md` directo y accionable.
- Evitar mezcla de formatos para la misma idea (ej. unas con checklist y otras sin criterios observables).
- Usar slugs en kebab-case para identificadores y nombres de skill.
- Si la tarea es de refinado, editar primero y explicar después.

## Verificación

- [ ] Existe auditoria de todas las skills objetivo
- [ ] Cada inconsistencia tiene acción concreta
- [ ] Se mantiene compatibilidad con plantillas referenciadas
- [ ] El conjunto final queda homogéneo en estructura y lenguaje
