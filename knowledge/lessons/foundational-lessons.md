# Lecciones fundacionales

Origen: extraídas directamente de la especificación fundacional de PIA (el documento que dio origen a esta skill), no de un proyecto ejecutado con un cliente real. Se documentan aquí como punto de partida porque ya son aprendizajes confirmados por quien diseñó la especificación — nuevas lecciones de proyectos reales deben añadirse siguiendo `workflows/retrospective.md`.

## Lección: La pregunta correcta ahorra más que diez preguntas genéricas

**Contexto de origen**: la especificación insiste en "agrupar las preguntas y limitarse a las más importantes" en vez de interrogar por partes.

**Lección**: cuando hace falta preguntar, una sola ronda con 2-3 preguntas realmente críticas produce mejor resultado y mejor experiencia que ir preguntando de a una a medida que surgen dudas menores.

**Generalización**: aplica a cualquier modo de PIA que empiece con descubrimiento (Crear, Convertir, Auditar cuando falta contexto sobre el propósito original).

---

## Lección: La crítica sin evidencia concreta no es crítica útil

**Contexto de origen**: la especificación exige que la revisión "busque fallos concretos, no críticas genéricas" desde las 6 perspectivas.

**Lección**: un hallazgo de revisión solo tiene valor accionable si señala ubicación, problema y el escenario de entrada que lo dispara. "Podría ser más claro" no es un hallazgo; "la regla de la sección 3 permite X, pero la sección 5 lo prohíbe cuando Y" sí lo es.

**Generalización**: aplica a `workflows/audit.md`, `templates/critic.md`, y a la Fase 6 de cualquier workflow de creación.

---

## Lección: Sobrediseñar es tan costoso como subdiseñar

**Contexto de origen**: principio 13-14 de la filosofía operativa original ("no sobrediseñar tareas simples", "no subdiseñar sistemas complejos").

**Lección**: la calidad de un artefacto de PIA no se mide por cuánta estructura tiene, sino por qué tan proporcional es esa estructura al tamaño real del problema. Un prompt de una línea con 9 fases explícitas documentadas es tan antipatrón como un sistema multiagente complejo reducido a un párrafo.

**Generalización**: aplica como criterio transversal en cualquier fase de arquitectura (Fase 3) de cualquier workflow.

---

## Lección: Una skill de Claude Code vale por lo que NO carga, no solo por lo que contiene

**Contexto de origen**: el diseño de esta misma skill PIA, que debió estructurar 8 referencias, 8 workflows, 12 plantillas, evaluaciones, ejemplos y base de conocimiento sin inflar `SKILL.md`.

**Lección**: el valor de una skill grande está en la progressive disclosure — `SKILL.md` actúa como índice operativo que dirige a la referencia correcta, no como contenedor de todo el conocimiento.

**Generalización**: aplica directamente a `references/skill-architecture.md` y a cualquier futura skill que PIA ayude a diseñar con múltiples carpetas de recursos.
