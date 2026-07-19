# Plantilla: Evaluador

Para un prompt o agente cuyo propósito es juzgar la calidad de otro artefacto o salida, no producir contenido nuevo. Ver `references/evaluation-framework.md`.

## Cuándo usar esta plantilla

Cuando se necesita un juicio consistente y repetible sobre si una salida cumple criterios definidos — por ejemplo, un LLM-judge que evalúa respuestas de otro sistema, o un evaluador de calidad de código.

## Plantilla

```text
# Identidad
{{Quién es el evaluador — no productor de contenido, sino juez.}}

# Qué evalúa
{{El tipo exacto de artefacto o salida que recibe.}}

# Criterios de evaluación
| Criterio | Qué significa 0 (falla completamente) | Qué significa 5 (ejemplar) |
|---|---|---|
| {{criterio 1}} | {{...}} | {{...}} |
| {{criterio 2}} | {{...}} | {{...}} |

# Reglas de juicio
- {{cómo pondera criterios entre sí, si alguno pesa más que otro}}
- {{qué hacer si dos criterios entran en conflicto}}
- El evaluador nunca corrige el artefacto evaluado por iniciativa propia — solo lo juzga, salvo que se le pida explícitamente una versión corregida.

# Evidencia obligatoria
Cada puntuación debe ir acompañada de una cita o referencia concreta del artefacto evaluado que la justifique — no una puntuación sin evidencia.

# Formato de salida
```text
Puntuación por criterio: {{criterio}}: {{0-5}} — {{evidencia}}
Veredicto global: {{aprobado / aprobado con reservas / rechazado}}
Razón del veredicto: {{...}}
```
```

## Ejemplo relleno (fragmento — evaluador de respuestas de soporte)

```text
# Criterios de evaluación
| Criterio | 0 | 5 |
|---|---|---|
| Precisión | Contiene información factualmente incorrecta | Toda la información es verificable y correcta |
| Tono | Grosero o condescendiente | Empático y profesional, sin ser artificial |
| Resolución | No aborda la pregunta del usuario | Resuelve completamente o deriva correctamente |
```

## Notas de uso

Un evaluador que no exige evidencia concreta por puntuación tiende a producir juicios inconsistentes entre ejecuciones — la sección "Evidencia obligatoria" no es opcional.
