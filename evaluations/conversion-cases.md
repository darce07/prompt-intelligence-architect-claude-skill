# Casos de evaluación: Conversión

Ver `workflows/convert.md`.

### Caso 9: Convertir un prompt en skill

**Entrada**: un prompt simple de ~30 líneas para "revisar documentación técnica y sugerir mejoras de claridad", junto con: "Convierte esto en una skill de Claude Code."

**Comportamiento esperado**: PIA no pega el texto original dentro de un `SKILL.md` sin más — añade lo que una skill necesita y un prompt no tiene: frontmatter con `description` orientada a activación, sección "cuándo se activa / cuándo no", y evalúa si el volumen de conocimiento justifica `references/`. El resultado sigue `references/skill-architecture.md`.

**Fallos prohibidos**:
- Entregar un `SKILL.md` que es solo el prompt original con un frontmatter pegado encima, sin cuándo-se-activa ni consideración de progressive disclosure.
- Inventar carpetas vacías o mencionadas pero sin contenido real.

**Criterios de aprobación**: El `SKILL.md` resultante tiene frontmatter válido con `name` y `description`, sección de activación/no-activación, y si se generan referencias adicionales, tienen contenido real (no placeholders).

---

### Caso 10: Adaptar una solución a Claude Code

**Entrada**: un agente diseñado originalmente como GPT personalizado (con Instructions + Knowledge + Actions separados), con: "Necesito esto funcionando en Claude Code."

**Comportamiento esperado**: PIA lee `references/platform-adaptation.md` sección 1, reestructura considerando `SKILL.md` vs. `CLAUDE.md` según si el comportamiento es reutilizable entre proyectos o específico de un repositorio, y no asume herramientas de Claude Code que el usuario no ha confirmado.

**Fallos prohibidos**: Asumir que Claude Code tiene exactamente las mismas "Actions" que el GPT original sin verificar qué herramientas están realmente disponibles en la sesión del usuario.

**Criterios de aprobación**: El artefacto resultante declara explícitamente qué herramientas asume y marca como supuesto (no como hecho confirmado) cualquier capacidad no verificada.

---

### Caso 11: Convertir un agente único en multiagente

**Entrada**: un agente único de "revisor de código" que en la práctica intenta cubrir seguridad, rendimiento y estilo a la vez, con resultados inconsistentes según qué aspecto prioriza cada vez. El usuario pide: "Divide esto en varios agentes especializados."

**Comportamiento esperado**: PIA no solo corta el texto en tres bloques — diseña roles con alcance no solapado, un orquestador o routing explícito, y una regla de consolidación/resolución de conflictos, siguiendo `references/multi-agent-architecture.md`.

**Fallos prohibidos**: Entregar tres prompts independientes sin ningún mecanismo de consolidación o resolución de conflictos entre sus hallazgos.

**Criterios de aprobación**: El sistema resultante tiene orquestador o routing explícito, y una regla concreta de qué pasa cuando dos roles no están de acuerdo.
