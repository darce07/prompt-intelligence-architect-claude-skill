# Base de conocimiento de PIA

Esta carpeta es la **única memoria persistente real** de Prompt Intelligence Architect. No hay aprendizaje automático oculto en ningún otro lugar: si un aprendizaje no está escrito aquí, PIA no lo recordará en la siguiente sesión.

Gobernanza completa en `references/continuous-improvement.md`. Resumen operativo:

- Nada se escribe aquí sin que PIA lo proponga primero al usuario (resumen o diff) y el usuario lo apruebe explícitamente.
- Cada adición debe ser repetible, generalizable, confirmada, útil en proyectos futuros, y libre de secretos o datos personales.
- Nunca se guarda: credenciales, datos personales, información confidencial, suposiciones no verificadas, preferencias de un solo proyecto disfrazadas de regla universal, código desactualizado sin contexto, o decisiones temporales sin fecha/versión.

## Subcarpetas

| Carpeta | Contenido | Cuándo añadir algo aquí |
|---|---|---|
| `patterns/` | Soluciones de diseño que funcionaron y se repitieron en más de un contexto | Cuando el mismo enfoque arquitectónico resolvió bien el mismo tipo de problema al menos dos veces |
| `anti-patterns/` | Errores confirmados que conviene evitar, con la razón | Cuando un enfoque falló de forma identificable y es probable que se repita si no se documenta |
| `lessons/` | Aprendizajes puntuales de un proyecto con valor generalizable, incluyendo el contexto que los hace válidos | Cuando algo funcionó o falló en un proyecto concreto y la lección trasciende ese proyecto, aunque no sea aún un patrón establecido |
| `platform-guides/` | Notas específicas de una plataforma (Claude Code, GPTs, Codex, Cursor/Windsurf/Copilot, Gemini) que no cambian con cada proyecto | Cuando se confirma un comportamiento o limitación real de una plataforma |
| `decision-records/` | ADRs — decisiones de arquitectura relevantes, con contexto y alternativas consideradas | Cuando una decisión de diseño no es obvia y merece quedar registrada para un mantenedor futuro |
| `glossary/` | Términos y su definición consistente dentro del dominio de PIA | Cuando un término se usa de forma ambigua o inconsistente y conviene fijar su significado |

## Cómo se aprueba y registra una lección nueva

1. PIA identifica el aprendizaje durante una tarea o retrospectiva (`workflows/retrospective.md`).
2. Verifica elegibilidad contra los criterios de arriba.
3. Redacta el fragmento exacto de texto propuesto.
4. Lo presenta al usuario, sin aplicarlo.
5. Solo tras aprobación explícita, escribe el archivo correspondiente.
6. Si el aprendizaje afecta comportamiento futuro de la skill (no solo un dato de referencia), se registra también en `CHANGELOG.md` con versión semántica.

## Estado actual

Los archivos de esta base de conocimiento se inicializaron junto con la creación de la skill, a partir de los principios ya presentes en la especificación original de PIA (no de proyectos reales ejecutados todavía). Están marcados como tal en cada archivo. Según se use PIA en proyectos reales, esta base debe crecer con aprendizajes confirmados siguiendo el protocolo de arriba.
