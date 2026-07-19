# Changelog

Formato de versionado semántico `MAJOR.MINOR.PATCH` según `references/continuous-improvement.md` sección 5. Cada entrada documenta fecha, tipo, motivo, impacto, compatibilidad y archivos afectados.

## [1.0.0] — 2026-07-19

**Tipo**: major (creación inicial)

**Motivo**: creación completa de la skill `prompt-intelligence-architect` a partir de la especificación fundacional "Prompt Intelligence Architect (PIA) — Especificación definitiva para Claude Code Skill Creator", cubriendo identidad, misión, filosofía operativa, modos de trabajo, flujo de 9 fases, estrategia de preguntas, arquitectura de salida, criterios de calidad, quality gates, sistema de crítica, base de conocimiento evolutiva, protocolo de aprendizaje continuo, versionado, seguridad y privacidad, compatibilidad de plataformas, biblioteca de plantillas, evaluaciones y antipatrones.

**Impacto**: skill nueva, sin comportamiento previo que romper.

**Compatibilidad**: N/A (primera versión).

**Archivos afectados**: todos — `SKILL.md`, `README.md`, `references/` (8 archivos), `workflows/` (8 archivos), `templates/` (12 archivos), `evaluations/` (6 archivos), `examples/` (5 archivos), `knowledge/` (README + 6 subcarpetas con contenido inicial).

---

## Cómo añadir una entrada nueva

1. Sigue el protocolo de `references/continuous-improvement.md` sección 4: propón el cambio antes de aplicarlo.
2. Determina el tipo (patch/minor/major) según la sección 5 de la misma referencia.
3. Añade una entrada nueva arriba de esta línea, con el mismo formato: fecha, tipo, motivo, impacto, compatibilidad, archivos afectados.
4. Si el cambio afecta comportamiento verificado por una evaluación existente, actualiza también `evaluations/`.
