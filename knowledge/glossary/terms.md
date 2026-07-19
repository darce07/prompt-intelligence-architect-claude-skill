# Glosario

Términos usados de forma consistente en toda la skill PIA. Si un término se usa de forma distinta en algún archivo, ese archivo tiene el error, no este glosario.

**Artefacto**: cualquier resultado que PIA produce — prompt simple, system prompt, agente, skill, sistema multiagente, `CLAUDE.md`, evaluador, crítico, etc.

**Modo**: la intención del usuario respecto a un artefacto (Crear, Mejorar, Auditar, Convertir, Simplificar, Expandir, Plantillizar, Enseñar, Diagnosticar, Evolucionar). Determina qué workflow de `workflows/` se sigue.

**Fase**: cada uno de los 9 pasos del flujo obligatorio de trabajo (Descubrimiento → Clasificación → Arquitectura → Diseño conductual → Construcción → Crítica adversarial → Refactorización → Entrega → Aprendizaje), descritos en `references/prompt-architecture.md`.

**Quality gate**: cada una de las 10 preguntas de verificación obligatoria antes de entregar un artefacto (ver `references/evaluation-framework.md` sección 3). Distinto de "criterio de calidad" (la puntuación 0-5 en 10 dimensiones, sección 2 de la misma referencia).

**Progressive disclosure**: el patrón de cargar información en capas (metadata siempre visible, cuerpo principal al activarse, recursos bajo demanda) para evitar consumir contexto innecesario. Ver `knowledge/patterns/architecture-patterns.md`.

**Contrato (entre agentes)**: la especificación explícita de qué formato de entrada espera un agente y qué formato de salida entrega, usada en sistemas multiagente para que la transición entre roles sea predecible. Ver `references/multi-agent-architecture.md` sección 3.

**Fundamentación**: la propiedad de que toda afirmación de un agente pueda respaldarse en una fuente verificable (documento recuperado, código real del repositorio) en vez de inventarse por plausibilidad. Central en agentes RAG y en agentes de documentación.

**Supuesto declarado**: una decisión que PIA toma en ausencia de confirmación explícita del usuario, y que comunica abiertamente en la entrega en vez de presentarla como un hecho confirmado.

**Aprendizaje gobernado**: el protocolo por el cual PIA propone cambios a `knowledge/` y los aplica solo tras aprobación explícita del usuario — nunca se autoedita en silencio. Ver `references/continuous-improvement.md`.

**Mínimo privilegio**: el principio de otorgar a un agente solo el nivel de acceso (lectura/escritura/ejecución) estrictamente necesario para su misión, nunca el máximo disponible "por si acaso".

**ADR (Architecture Decision Record)**: documento que registra una decisión de arquitectura relevante, su contexto, las alternativas consideradas y cuándo reconsiderarla. Ver `templates/adr.md`.
