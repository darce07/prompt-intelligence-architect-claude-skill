# Workflow: Crear

Cuándo usarlo: el usuario pide un artefacto nuevo desde cero — "créame un prompt para...", "necesito un agente que...", "diseña una skill para...", "quiero un sistema multiagente".

## Pasos

1. **Descubrimiento** (Fase 1 de `references/prompt-architecture.md`). Extrae del mensaje del usuario todo lo que ya está implícito antes de preguntar nada. Si falta información crítica (ver "Estrategia de preguntas"), pregunta agrupado; si no, infiere y declara supuestos.

2. **Clasificación** (Fase 2). Decide el tipo de artefacto: prompt simple, system prompt, agente, skill, multiagente, etc. Esto determina qué referencia leer:
   - Prompt simple/system → `references/prompt-architecture.md`
   - Agente → `references/agent-architecture.md`
   - Skill de Claude Code → `references/skill-architecture.md`
   - Multiagente → `references/multi-agent-architecture.md`
   - Si el destino no es Claude Code → añade `references/platform-adaptation.md`

3. **Arquitectura** (Fase 3). Antes de escribir una sola línea del artefacto, decide: monolítico o modular, qué archivos hacen falta, roles, flujo, entradas/salidas, herramientas, memoria, si necesita evaluaciones.

4. **Diseño conductual** (Fase 4). Define identidad, misión, límites, manejo de ambigüedad y errores, tono, formato de respuesta, criterios de escalamiento — antes de redactar el texto final.

5. **Construcción** (Fase 5). Usa la plantilla de `templates/` que corresponda al tipo clasificado como punto de partida. Adáptala siempre al caso — nunca la entregues sin personalizar.

6. **Crítica adversarial** (Fase 6). Aplica las 6 perspectivas y los 10 quality gates de `references/evaluation-framework.md`. Si el artefacto toca archivos, herramientas, RAG o datos sensibles, aplica también el checklist de `references/security-and-privacy.md`.

7. **Refactorización** (Fase 7). Corrige lo que la crítica encontró. No añadas cambios cosméticos que no resuelvan un hallazgo real.

8. **Entrega** (Fase 8) usando el formato siguiente.

## Formato de respuesta

```text
Diagnóstico breve          — qué necesita realmente el usuario, en 2-4 líneas
Arquitectura elegida        — qué tipo de artefacto y por qué esa estructura
Artefacto final              — el contenido completo, listo para usar
Cómo usarlo                   — instrucciones de instalación/activación si aplica
Criterios de validación        — cómo puede el usuario comprobar que funciona
```

## Fallos prohibidos en este workflow

- Entregar un prompt genérico ("actúa como experto en X") sin pasar por Fase 3-4.
- Preguntar más de una ronda de preguntas cuando la primera ya cubría lo crítico.
- Sobrediseñar (multiagente, memoria persistente, herramientas extensas) una tarea que un prompt simple resuelve.
- Omitir la Fase 6 y entregar sin crítica adversarial.
