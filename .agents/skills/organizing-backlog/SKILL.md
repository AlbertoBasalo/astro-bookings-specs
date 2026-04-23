---
name: organizing-backlog
description: Organiza el backlog de un proyecto de software, priorizando especificaciones según sus dependencias y estado. Usar cuando se crea una especificación nueva o se actualiza el estado de una existente.
---

# Organizar backlog

## Rol 

Actúa como un Product Owner o Scrum Master responsable de organizar el backlog de un proyecto de software.

## Tarea

Organizar el backlog del proyecto, priorizando las especificaciones según sus dependencias y estado.

## Contexto

- PRD disponible en `{Project_Folder}/PRD.md`.
- Especificaciones en `{Project_Folder}/specs/` 
- Backlog (si ya existe) en `{Project_Folder}/BACKLOG.md`.

## Pasos

### 1. Preguntas aclaratorias

Haz preguntas solo si bloquean decisiones del documento:
- No encuentras PRD o especificaciones
- No está claro el estado o dependencias de alguna especificación

### 2. Redacción del backlog

Genera el documento de backlog siguiendo la plantilla basada en el idioma del usuario:

- [En español (Spanish)](backlog.template.md)  


Reglas:
- Usa el identificador compuesto `{id-slug}` como clave única.
- En la columna de dependencias, usa los identificadores cortos `[FR1, FR2]`
- Las especificaciones pasan por los siguientes estados:
  - `Pendiente`: aún no se ha comenzado a trabajar en la especificación.
  - `En Curso`: se está trabajando activamente en la especificación.
  - `Completada`: se ha finalizado el trabajo en la especificación.
  - `Bloqueada`: en espera debido a dependencias no resueltas.
  - `Fallida`: el trabajo en la especificación no se ha podido completar.

## Verificación

- [ ] Backlog actualizado en `{Project_Folder}/BACKLOG.md`
- [ ] Contiene todas las especificaciones
- [ ] Cada una con sus dependencias y estado actualizados
