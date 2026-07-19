# ADR-001: Alcance inicial de Prompt Intelligence Architect

Fecha: 2026-07-19
Estado: aceptado

## Contexto

Al crear la skill PIA a partir de la especificación fundacional, había que decidir si construir un `SKILL.md` único y extenso, o una estructura modular completa (references/workflows/templates/evaluations/examples/knowledge) desde el primer momento.

## Decisión

Se construyó la estructura modular completa desde el inicio, siguiendo el árbol de archivos especificado en la fuente original, en vez de empezar con un `SKILL.md` monolítico e ir extrayendo secciones después.

## Alternativas consideradas

- `SKILL.md` único y extenso con todo el contenido — descartada porque la especificación fundacional exige explícitamente evitar un "prompt monolítico" y porque el volumen de conocimiento (9 fases, 10 quality gates, arquitectura de 4 tipos de artefacto, seguridad, versionado, biblioteca de plantillas) excede ampliamente el límite recomendado de ~500 líneas para el cuerpo de una skill.
- Estructura modular parcial (solo `references/`, sin `workflows/` ni `templates/` separados) — descartada porque la especificación pide explícitamente workflows por modo de trabajo y una biblioteca de plantillas reutilizables como entregables independientes.

## Consecuencias

Positivas:
- `SKILL.md` se mantiene compacto y operativo, apuntando a referencias en vez de duplicarlas.
- Cada tipo de artefacto (prompt, agente, skill, multiagente) tiene su propia referencia y plantilla, facilitando mantenimiento independiente.

Negativas o trade-offs aceptados:
- Mayor número de archivos a mantener coherentes entre sí; un cambio de comportamiento fundamental puede requerir tocar varios archivos (`SKILL.md`, la referencia correspondiente, y posiblemente una evaluación).

## Cuándo reconsiderar esta decisión

Si en el uso real se observa que la estructura modular genera fricción desproporcionada para tareas pequeñas, o si Claude Code cambia su mecanismo de carga de recursos de forma que la progressive disclosure deje de aportar el beneficio esperado.
