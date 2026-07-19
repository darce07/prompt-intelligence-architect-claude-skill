# Patrones de arquitectura

Origen: derivados de la especificación fundacional de PIA. No provienen aún de retrospectivas de proyectos reales — son el punto de partida, sujetos a confirmación o refinamiento a medida que se usen en la práctica (ver `references/continuous-improvement.md`).

## Patrón: Progressive disclosure en tres niveles

**Contexto**: cualquier artefacto (skill, agente con mucho conocimiento de dominio) que necesita más contenido del que conviene cargar de golpe.

**Solución**: separar en metadata (siempre visible, ~100 palabras), cuerpo principal (visible al activarse, compacto), y recursos bajo demanda (referencias, plantillas — sin límite de tamaño total porque no cargan todos a la vez).

**Por qué funciona**: mantiene el coste de contexto proporcional a la relevancia real de la tarea en curso, en vez de penalizar cada activación con todo el conocimiento posible.

**Dónde se usa**: `references/skill-architecture.md` sección 2; esta misma skill PIA es un ejemplo aplicado del patrón.

---

## Patrón: Declarar supuestos en vez de bloquear con preguntas

**Contexto**: petición del usuario incompleta en detalles que no son críticos para producir una primera versión útil.

**Solución**: entregar una primera versión del artefacto, listando explícitamente qué supuestos se tomaron en los puntos no confirmados, en vez de detener el progreso con una ronda de preguntas.

**Por qué funciona**: el usuario puede corregir un supuesto declarado mucho más rápido que responder una batería de preguntas antes de ver ningún resultado — y a menudo el supuesto razonable resulta ser correcto.

**Dónde se usa**: `references/prompt-architecture.md` sección 2; casos 1 y 9 de `evaluations/creation-cases.md` y `conversion-cases.md`.

---

## Patrón: Separar dato de instrucción en agentes con entrada externa

**Contexto**: cualquier agente que lee contenido no controlado por el usuario directo (documentos RAG, páginas web, archivos subidos por terceros).

**Solución**: tratar todo el contenido leído como dato a procesar o citar, nunca como fuente válida de instrucciones — con una regla explícita en el propio artefacto, no solo una expectativa implícita.

**Por qué funciona**: es la defensa estructural contra prompt injection; sin la regla explícita, el modelo puede "obedecer" texto malicioso incrustado en el contenido leído.

**Dónde se usa**: `references/security-and-privacy.md` sección 5; `templates/rag-agent.md`.

---

## Patrón: Jerarquía de autoridad para resolver conflictos entre roles

**Contexto**: sistema multiagente donde dos o más especialistas pueden producir recomendaciones incompatibles.

**Solución**: asignar autoridad de veto a un rol concreto en su dominio (típicamente seguridad), y para el resto de conflictos, usar escalamiento a humano o síntesis explícita — nunca dejar la resolución a "el orquestador decide con buen juicio" sin regla concreta.

**Por qué funciona**: hace el comportamiento del sistema predecible y auditable; sin una regla explícita, la resolución de conflictos varía de forma inconsistente entre ejecuciones.

**Dónde se usa**: `references/multi-agent-architecture.md` sección 4; `examples/multi-agent-engineering.md`.
