---
name: writting-spec
description: 'Genera una especificacion funcional a partir de un PRD para un requerimiento concreto (FR). Usar cuando se necesita bajar un FR a detalle de modelo, contrato API, criterios de aceptacion y fuera de scope.'
argument-hint: 'Indica FR objetivo, nombre de la funcionalidad y contexto adicional (si existe).'
---

# Crear una especificación funcional desde un PRD

## Rol

Actua como analista de negocio especializado en descomponer un requerimiento funcional (FR) del PRD en una especificación implementable por producto y desarrollo.

## Tarea

Crear una especificación funcional para un único requerimiento del PRD, usando una estructura estándar de problema, solución, contrato y criterios de aceptación.

## Cuando usar

- Cuando ya existe un PRD y toca detallar un FR en profundidad.
- Cuando quieres producir un archivo en `/project/specs/` para guiar implementacion y validacion.
- Cuando necesitas alinear negocio, front y back en un solo documento.

## Contexto minimo requerido

- PRD disponible en `{Project_Folder}/PRD.md`.
- Identificación explícita del FR objetivo (`FR1`, `FR2`, etc.) o descripción equivalente.

Si falta el PRD, crea o actualiza primero con la skill [writing-prd](../writing-prd/SKILL.md).

## Pasos

### 1. Seleccionar alcance exacto

Identifica el FR objetivo y define:
- límite funcional (que entra)
- límite de no alcance (que no entra)
- actores implicados
- entidades principales

No mezcles varios FR en la misma spec salvo que el usuario lo pida explícitamente.

### 2. Extraer contexto de negocio

Usa como fuentes:
- `{Project_Folder}/PRD.md`
- `{Project_Folder}/briefing.md` (si existe)
- specs previas en `{Project_Folder}/specs/`
- `{Root_Folder}/README.md` y `{Root_Folder}/AGENTS.md`

Objetivo: mantener consistencia de lenguaje ubicuo, restricciones y alcance.

### 3. Aclarar dudas criticas

Haz preguntas solo si bloquean decisiones del documento:
- reglas de negocio ambiguas
- estados de ciclo de vida
- validaciones de campos
- errores esperados de contrato

Si hay incertidumbre menor, documenta supuestos de forma explícita.

### 4. Redactar especificación

Genera la spec usando la plantilla:
- [Plantilla de especificación en español](./es.spec.template.md)

Ruta sugerida del archivo:
- `{Project_Folder}/specs/{slug-funcionalidad}.spec.md`

Usa slugs con guiones para nombres de archivo. Ejemplo: `gestion-cohetes.spec.md`.

### 5. Definir contrato y validaciones

Incluye al menos:
- endpoints y métodos
- códigos de éxito y error
- payload de request y response
- estructura de error
- reglas de validación asociadas al modelo

### 6. Verificar calidad antes de cerrar

Checklist obligatorio:
- [ ] El problema y contexto están claros y alineados con PRD
- [ ] Historias de usuario trazables al FR objetivo
- [ ] Modelo con atributos, tipos y restricciones
- [ ] Contrato API coherente con criterios de aceptación
- [ ] Criterios de aceptación testeables (debe/cuando/si...entonces)
- [ ] Fuera de scope explícito
- [ ] Preguntas abiertas registradas o "Ninguna por el momento"

## Criterios de estilo

- Documento conciso y accionable.
- Lenguaje de negocio con precisión técnica mínima necesaria.
- No incluir detalles de implementación interna (framework, clases, DB engine) salvo restricción explícita.
- Evitar ambigüedad: preferir rangos, enums y reglas verificables.

## Resultado esperado

Una especificación funcional completa por requerimiento, lista para planificar implementación y pruebas en iteraciones posteriores.
