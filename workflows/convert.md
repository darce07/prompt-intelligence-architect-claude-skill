# Workflow: Convertir

Cuándo usarlo: el usuario pide transformar un artefacto de un formato o plataforma a otro — "convierte este prompt en una skill", "pasa esto a CLAUDE.md", "convierte este agente único en multiagente".

## Pasos

1. **Identifica el formato origen y destino explícitamente.** No asumas el destino si no está claro (pregunta si es ambiguo y material para el resultado — ver `references/prompt-architecture.md`, sección 2).

2. **Extrae la intención y el comportamiento del artefacto origen**, no solo su texto literal. Convertir no es "pegar el mismo texto en otra plantilla" — es preservar el comportamiento en la arquitectura del nuevo formato.

3. **Lee la referencia del formato destino:**
   - A skill → `references/skill-architecture.md`
   - A `CLAUDE.md` → `templates/claude-md.md` y las notas de la sección 1 de `references/platform-adaptation.md`
   - A agente → `references/agent-architecture.md`
   - A multiagente → `references/multi-agent-architecture.md`
   - A otra plataforma (GPT, Codex, Cursor, Gemini) → `references/platform-adaptation.md`

4. **Rediseña, no traduzcas literalmente.** Cada formato tiene su propia anatomía (ver referencias). Un prompt simple convertido a skill necesita ganar: cuándo se activa/no se activa, estructura de carpetas si aplica, progressive disclosure. Un agente único convertido a multiagente necesita roles separados y contratos entre ellos, no solo dividir el texto en dos.

5. **Verifica qué se pierde o gana en la conversión** y decláralo: por ejemplo, convertir una skill a `CLAUDE.md` pierde la activación selectiva (todo se carga siempre); conviene advertirlo.

6. **Aplica la crítica adversarial** del formato destino antes de entregar (`references/evaluation-framework.md`).

## Formato de respuesta

Usa el formato "Crear" (`workflows/create.md`) ya que el resultado es, para todos los efectos, un artefacto nuevo en el formato destino — pero añade una sección extra:

```text
Diagnóstico breve
Arquitectura elegida
Qué se preserva / qué cambia respecto al original   ← específico de este workflow
Artefacto final
Cómo usarlo
Criterios de validación
```

## Fallos prohibidos en este workflow

- Traducir literalmente sin adaptar a la anatomía real del formato destino (por ejemplo, entregar una "skill" que es solo el prompt original pegado en un `SKILL.md` sin cuándo-se-activa ni estructura).
- No declarar qué capacidades se pierden o ganan en la conversión.
- Inventar sintaxis de la plataforma destino no confirmada (ver `references/platform-adaptation.md`, sección 6).
