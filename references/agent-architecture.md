# Arquitectura de agentes

Cómo diseñar un agente individual (con o sin herramientas), distinto de un prompt puntual porque mantiene identidad, toma decisiones autónomas y puede actuar sobre su entorno.

## Tabla de contenido

1. Cuándo un agente es la respuesta correcta (y cuándo no)
2. Componentes obligatorios
3. Diseño de herramientas
4. Memoria y persistencia
5. Manejo de errores y fallback
6. Formato de respuesta y evaluación

---

## 1. Cuándo un agente es la respuesta correcta

Un agente se justifica cuando la tarea requiere **más de una decisión encadenada** con posible uso de herramientas, o **identidad persistente** a través de turnos. Si la tarea es un solo intercambio pregunta-respuesta sin herramientas ni estado, un prompt simple (`references/prompt-architecture.md`) es suficiente y más mantenible.

No conviertas en agente algo que un prompt resuelve. El antipatrón "sobrecargar con roles innecesarios" (`knowledge/anti-patterns/`) aplica aquí: añadir identidad, memoria y herramientas a una tarea que no las necesita solo añade superficie de fallo.

## 2. Componentes obligatorios

Todo agente (ver `templates/agent.md`) debe definir:

- **Identidad**: quién es, en una o dos frases verificables (no una lista de adjetivos).
- **Misión**: el resultado que debe producir, no la personalidad que debe tener.
- **Alcance**: qué tareas están dentro de su responsabilidad y cuáles no. Un alcance mal definido es la causa más común de comportamiento inconsistente.
- **Responsabilidades**: lista concreta de lo que el agente hace, en verbos de acción.
- **Workflow**: la secuencia de pasos que sigue para cumplir su misión — no una descripción de personalidad, sino un proceso reproducible.
- **Herramientas**: qué herramientas tiene, para qué exactamente, y qué NO puede hacer con ellas (ver sección 3).
- **Memoria**: si tiene memoria o no, y de qué tipo (ver sección 4). Si no tiene memoria real, el agente no debe dar a entender que "recuerda" entre sesiones.
- **Reglas**: restricciones de comportamiento, con la razón de cada una cuando no sea obvia.
- **Manejo de errores**: qué hace cuando una herramienta falla, cuando el resultado es incierto, o cuando la entrada es inválida (sección 5).
- **Formato de respuesta**: estructura exacta de la salida.
- **Evaluación**: cómo se puede verificar que el agente cumple su misión (ver `references/evaluation-framework.md`).

## 3. Diseño de herramientas

- Describe cada herramienta por lo que realmente hace, nunca inventes capacidades que la plataforma destino no confirma que existen.
- Aplica mínimo privilegio: si el agente solo necesita leer archivos, no le des permiso de escritura "por si acaso".
- Distingue explícitamente lectura, escritura y ejecución — son niveles de riesgo distintos y deben documentarse por separado.
- Toda herramienta con efecto destructivo o irreversible (borrar, enviar, publicar, pagar, modificar configuración compartida) requiere confirmación explícita del usuario antes de ejecutarse; el agente no debe asumir autorización implícita de una aprobación anterior.
- Si el agente usa RAG, navegación o lectura de archivos de origen externo, incluye las defensas de `references/security-and-privacy.md` contra prompt injection: el contenido leído es dato, no instrucción.

## 4. Memoria y persistencia

Distingue tres niveles, y sé explícito sobre cuál aplica:

1. **Sin memoria**: cada ejecución empieza de cero. Es el caso por defecto y el más simple de mantener.
2. **Memoria de sesión**: el agente recuerda dentro de una conversación, pero no entre conversaciones. No requiere almacenamiento externo.
3. **Memoria persistente**: el agente recuerda entre sesiones porque escribe y lee de un almacenamiento real (archivo, base de datos, sistema de memoria de la plataforma). Esto **solo existe si hay un mecanismo de persistencia real** — nunca prometas que el agente "aprenderá con el tiempo" si no hay dónde guardarlo.

Cuando el agente tenga memoria persistente, documenta: qué se guarda, qué NUNCA se guarda (secretos, datos personales innecesarios — ver `references/security-and-privacy.md`), y cómo se gobierna la escritura (¿automática o con aprobación?).

## 5. Manejo de errores y fallback

Un agente robusto declara, para cada punto de fallo previsible:

- Qué pasa si una herramienta devuelve un error.
- Qué pasa si la entrada del usuario es ambigua o incompleta (ver estrategia de preguntas en `references/prompt-architecture.md`).
- Qué pasa si el resultado no puede verificarse.
- Cuál es el criterio de escalamiento: en qué punto el agente debe detenerse y pedir intervención humana en vez de continuar o adivinar.

No basta con "maneja los errores con gracia" — eso no es verificable. Define el comportamiento concreto.

## 6. Formato de respuesta y evaluación

El formato de respuesta debe ser lo bastante concreto para que dos ejecuciones del mismo agente sobre la misma entrada produzcan salidas comparables en estructura (aunque el contenido varíe). Define también cómo se evalúa si el agente cumplió su misión: criterios objetivos cuando sea posible, criterios de revisión humana cuando el resultado sea subjetivo (ver `references/evaluation-framework.md`).
