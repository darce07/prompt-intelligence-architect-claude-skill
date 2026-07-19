# Casos de evaluación: Creación

Ver `workflows/create.md` y `references/evaluation-framework.md`.

### Caso 1: Crear desde una necesidad vaga

**Entrada**: "Necesito un prompt para que Claude revise mi frontend."

**Comportamiento esperado**: PIA detecta que faltan datos críticos (stack tecnológico, alcance de la revisión, criterios de calidad) pero no bloquea el avance. O bien hace una ronda breve y agrupada de preguntas sobre lo crítico, o entrega una primera versión declarando explícitamente los supuestos que tomó (por ejemplo, "asumo React + revisión de accesibilidad y rendimiento; ajústalo si tu stack es distinto"). El artefacto entregado tiene rol, alcance, flujo, criterios de severidad, formato de salida y límites — no es una sola frase de "actúa como experto".

**Fallos prohibidos**:
- Responder únicamente con algo equivalente a "Actúa como experto frontend y revisa mi código" sin arquitectura real.
- Bloquear el avance con una lista larga de preguntas antes de ofrecer cualquier valor.
- Inventar un stack tecnológico específico sin declararlo como supuesto.

**Criterios de aprobación**: El artefacto entregado tiene, como mínimo, rol, alcance, criterios de revisión, formato de salida y niveles de severidad. Si se hicieron preguntas, están agrupadas en una sola ronda y limitadas a lo crítico.

---

### Caso 2: Diseñar un agente con herramientas

**Entrada**: "Quiero un agente que lea archivos de un repositorio y me sugiera qué tests faltan, sin que pueda escribir código."

**Comportamiento esperado**: PIA usa `templates/tool-agent.md` o `templates/agent.md`, declara explícitamente el nivel de acceso (solo lectura), documenta qué NO puede hacer con las herramientas (escritura, ejecución), y define manejo de errores y formato de salida.

**Fallos prohibidos**:
- Otorgar al agente permisos de escritura "por si acaso" o "para que sea más útil", contradiciendo la restricción explícita del usuario.
- Inventar una herramienta de análisis de cobertura de tests que la plataforma no tiene confirmada.

**Criterios de aprobación**: El inventario de herramientas del artefacto entregado lista explícitamente solo lectura, y hay una nota explícita de que no tiene ni necesita permisos de escritura.

---

### Caso 3: Diseñar un sistema multiagente

**Entrada**: "Necesito un sistema con un orquestador y especialistas en seguridad, rendimiento y accesibilidad para revisar pull requests."

**Comportamiento esperado**: PIA valida primero (implícita o explícitamente) que el caso justifica multiagente (tres dominios de conocimiento distintos, posible paralelismo). Entrega roles con alcance no solapado, routing explícito, contrato de entrada/salida entre roles, y una regla de resolución de conflictos concreta (no "el orquestador usa buen juicio").

**Fallos prohibidos**:
- Fusionar los tres especialistas en un solo rol con instrucciones mezcladas.
- Dejar la resolución de conflictos sin regla concreta.
- No definir qué pasa si un rol no tiene hallazgos (contrato de salida vacío no definido).

**Criterios de aprobación**: Existen tres roles con alcance diferenciado, una tabla de routing, y una regla explícita de resolución de conflictos (jerarquía, escalamiento o síntesis).

---

### Caso 4: Explicar la elección de arquitectura

**Entrada**: "¿Por qué elegiste un solo agente en vez de varios para esto?"

**Comportamiento esperado**: PIA explica la decisión en términos de los criterios reales de `references/multi-agent-architecture.md` sección 1 (dominios distintos, paralelismo real, necesidad de auditoría independiente) aplicados al caso concreto — no una respuesta genérica de "es más simple".

**Fallos prohibidos**: Justificación vaga sin referencia a los criterios concretos que hicieron la diferencia en ese caso específico.

**Criterios de aprobación**: La explicación cita al menos un criterio concreto de la referencia y lo conecta con un detalle específico de la tarea del usuario.
