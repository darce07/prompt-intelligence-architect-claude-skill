# Workflow: Retrospectiva

Cuándo usarlo: al cerrar un proyecto o tarea significativa de diseño de instrucciones, para capturar aprendizajes reutilizables. No es un workflow que se ejecuta en cada interacción — solo cuando hay un aprendizaje genuino que vale la pena persistir. Ver el protocolo completo en `references/continuous-improvement.md`.

## Pasos

1. **Confirma que hay algo que vale la pena capturar.** No toda tarea termina en un aprendizaje nuevo. Si el proyecto simplemente aplicó patrones ya conocidos sin sorpresas, no fuerces la retrospectiva.

2. **Recorre las preguntas de la retrospectiva** (sección 2 de `references/continuous-improvement.md`): necesidad real resuelta, qué patrón funcionó, qué falló, qué ambigüedad se repitió, qué estructura fue reusable, qué antipatrón quedó demostrado, qué decisión merece un ADR, qué conocimiento quedó obsoleto, qué mejora necesita la propia skill PIA.

3. **Filtra por elegibilidad** usando la lista de "qué guardar y qué no" (sección 3 de `references/continuous-improvement.md`). Descarta cualquier candidato que sea información sensible, una preferencia de un solo proyecto, o una suposición no confirmada.

4. **Redacta la propuesta concreta** para cada aprendizaje elegible: el fragmento exacto de texto que se añadiría a `knowledge/patterns/`, `knowledge/anti-patterns/`, `knowledge/lessons/`, `knowledge/platform-guides/`, `knowledge/decision-records/` o `knowledge/glossary/`.

5. **Presenta la propuesta al usuario** de forma explícita, sin aplicar el cambio todavía.

6. **Aplica solo tras aprobación explícita**, y actualiza `CHANGELOG.md` si el aprendizaje afecta el comportamiento futuro de la skill (por ejemplo, un antipatrón nuevo que cambiará cómo PIA diseña en el futuro).

## Formato de respuesta

```text
Resumen del proyecto              — en 2-3 líneas, qué se construyó
Aprendizajes candidatos             — cada uno con su categoría (patrón/antipatrón/lección/guía/ADR)
Propuesta de cambio a knowledge/       — el texto exacto a añadir, por archivo
Pendiente de tu aprobación               — recordatorio explícito de que nada se ha escrito aún
```

## Fallos prohibidos en este workflow

- Escribir en `knowledge/` sin que el usuario haya aprobado explícitamente la propuesta.
- Forzar una retrospectiva cuando no hay ningún aprendizaje genuino que capturar.
- Proponer como "patrón universal" algo que solo se probó una vez en un contexto muy específico — eso es una hipótesis, no un patrón confirmado.
