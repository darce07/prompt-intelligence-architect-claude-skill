# Plantilla: Skill de Claude Code

Ver `references/skill-architecture.md` para la anatomía completa. Esta plantilla cubre el `SKILL.md` mínimo; para skills grandes añade la estructura de carpetas descrita en esa referencia.

## Cuándo usar esta plantilla

Cuando el comportamiento es reutilizable entre proyectos o tareas, y el conocimiento necesario justifica activación bajo demanda en vez de vivir en un prompt único o en `CLAUDE.md`.

## Plantilla de `SKILL.md`

```text
---
name: {{nombre-en-kebab-case}}
description: {{Qué hace, para qué contextos se activa, y frases de ejemplo que
un usuario real escribiría. Sé deliberadamente específico e "insistente" —
declara también cuándo NO se activa si hay riesgo de falso positivo con una
tarea cercana.}}
---

# {{Nombre legible de la skill}}

{{Identidad/propósito en 2-4 líneas.}}

## Cuándo se activa
{{Lista de contextos/frases de disparo.}}

## Cuándo NO se activa
{{Casos cercanos que NO deben disparar esta skill.}}

## Flujo de decisión
{{Cómo pasar de la petición del usuario a la referencia/plantilla correcta —
normalmente una tabla "si la tarea es X, lee Y".}}

## Reglas fundamentales
1. {{regla}}
2. {{regla}}
...

## Formato de respuesta
{{Estructura esperada de la salida de esta skill.}}

## Protocolo de aprendizaje (si aplica)
{{Cómo se propone y aprueba un cambio a la base de conocimiento de la skill.}}

## Límites de seguridad
{{Qué la skill nunca debe hacer.}}

## Ejemplos cortos de activación
- "{{frase de ejemplo 1}}"
- "{{frase de ejemplo 2}}"
```

## Estructura de carpetas sugerida (skills medianas/grandes)

```text
{{nombre-skill}}/
├── SKILL.md
├── README.md
├── references/
├── workflows/         (si la skill tiene múltiples modos)
├── templates/          (si genera artefactos reutilizables)
├── examples/
├── evaluations/
└── knowledge/            (solo si la skill acumula aprendizaje real y gobernado)
```

## Notas de uso

No copies esta plantilla completa para una skill pequeña de un solo propósito — un `SKILL.md` autocontenido de 50-100 líneas sin carpetas adicionales es perfectamente válido si no hay conocimiento profundo que justifique `references/`. Escala la estructura al tamaño real (ver `references/skill-architecture.md`, sección 4).
