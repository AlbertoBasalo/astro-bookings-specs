---
name: writing-spec
description: Redacta una especificación funcional de un requerimiento concreto a partir de un PRD. Usar cuando se necesita bajar un requerimiento a detalle de modelo, contrato API, criterios de aceptación y fuera de scope.
---

# Crear una especificación funcional desde un PRD

## Rol

Actúa como analista de negocio especializado en descomponer un requerimiento.
Convierte un requerimiento funcional (FR) o técnico (TR) del PRD en una especificación implementable por producto y desarrollo.

## Tarea

Crear una especificación funcional para un único requerimiento del PRD, usando una estructura estándar de problema, solución, verificación..

## Contexto

- Briefing en `{Project_Folder}/briefing.md`
- PRD disponible en `{Project_Folder}/PRD.md`.
- Identificación explícita del FR o TR objetivo (`FR1`, `FR2`, `TR1`, `TR2`, etc.) o descripción equivalente.

Si falta el PRD, crea uno primero con la skill [writing-prd](../writing-prd/SKILL.md).

## Pasos

### 1. Preguntas aclaratorias

Haz preguntas solo si bloquean decisiones del documento:
- identificación clara del FR/TR objetivo
- alcance funcional (qué debe hacer el sistema)
- reglas de negocio ambiguas
- estados de ciclo de vida
- validaciones de campos
- errores esperados de contrato

Si hay incertidumbre menor, documenta supuestos de forma explícita.

No mezcles varios FR/TR en la misma spec salvo que el usuario lo pida explícitamente.

### 2. Redacción de la especificación

Genera la spec usando la plantilla:
- [Plantilla de especificación en español](./es.spec.template.md)

#### 2.1 Identificador y slug

- Asigna un identificador único a la spec basado en su requerimiento(ej. `FR1`, `TR2`) 
- Complétalo con un slug descriptivo en kebab-case (ej. `gestion-cohetes`).

El nombre del archivo debe ser una combinación de ambos: `{id-slug}.spec.md`. Ejemplo: `FR1-gestion-cohetes.spec.md`.
- `{Project_Folder}/specs/{id-slug}.spec.md`

#### 2.2 Reglas de contenido

- Problema: describe el contexto, historias de usuario, entidades y reglas de negocio.
- Solución: sin detalles técnicos, describe qué se debe hacer en cada capa física (UI, API, DB)
- Verificación: criterios de aceptación en formato Easy Approach to Requirements Syntax (EARS) 

## Verificación

- [ ] Especificación completa en `{Project_Folder}/specs/{id-slug}.spec.md`
- [ ] Basada en un único requerimiento del PRD
- [ ] Estructura clara de problema, solución y verificación

