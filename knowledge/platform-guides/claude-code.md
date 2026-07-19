# Guía de plataforma: Claude Code

Notas confirmadas sobre Claude Code relevantes para el diseño de artefactos. Complementa `references/platform-adaptation.md` sección 1 — esta guía documenta hechos de plataforma estables, no el proceso de adaptación en sí.

## Mecanismos de instrucciones disponibles

- **`CLAUDE.md`**: se carga automáticamente para el repositorio en el que se trabaja. Puede existir en la raíz y en subcarpetas para reglas de alcance más específico. Es el lugar correcto para convenciones y comandos que aplican siempre en ese repositorio — no para comportamiento ocasional.
- **Skills (`SKILL.md` + recursos)**: se activan bajo demanda según coincidencia entre la petición del usuario y la `description` del frontmatter. Pueden vivir a nivel usuario (`~/.claude/skills/`, disponibles en cualquier repositorio) o a nivel proyecto (`.claude/skills/` dentro del repositorio, específicas de ese proyecto).
- **Herramientas**: varían según la sesión y la configuración del usuario (Bash, Read, Edit, Grep, Glob, MCP servers específicos, etc.). No hay un conjunto universal garantizado — un artefacto que asuma una herramienta concreta debe declararlo como supuesto si no está confirmado.

## Observaciones sobre activación de skills

- La `description` del frontmatter es el mecanismo principal de activación. Los modelos tienden a subactivar skills cuando la descripción es vaga — una descripción específica, con ejemplos de frases de disparo, reduce falsos negativos.
- Declarar explícitamente cuándo NO se activa reduce falsos positivos con tareas cercanas.

## Límites conocidos (a confirmar caso por caso)

- No existe garantía de que una skill tenga acceso a subagentes, navegador, o herramientas MCP específicas salvo que la configuración del usuario las incluya — no lo asumas al diseñar para un usuario cuyo entorno no conoces.
- El tamaño de `SKILL.md` no tiene un límite estricto impuesto por la plataforma, pero superar ~500 líneas degrada la proporción señal/ruido de cada activación — es una guía de diseño, no una restricción técnica dura.

## Notas de esta entrada

Esta guía documenta comportamiento de plataforma tal como se entendía al momento de crear esta skill (2026). Claude Code evoluciona; si se detecta que algo aquí quedó desactualizado, debe corregirse siguiendo el protocolo de `references/continuous-improvement.md` en vez de dejarlo como referencia obsoleta.
