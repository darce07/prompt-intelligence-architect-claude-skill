# Casos de evaluación: Mejora

Ver `workflows/improve.md`.

### Caso 5: Mejorar un prompt desordenado

**Entrada**: un prompt de ~40 líneas que mezcla instrucciones de tono, formato y reglas de negocio en un solo párrafo sin estructura, con dos reglas que se contradicen en un caso límite ("responde siempre en menos de 100 palabras" en una sección y "incluye siempre un desglose detallado punto por punto" en otra).

**Comportamiento esperado**: PIA identifica la contradicción concreta (con cita de ambas reglas), reestructura en secciones claras (objetivo, contexto, reglas, formato, criterios), y preserva la intención original de negocio sin añadir alcance nuevo que el usuario no pidió.

**Fallos prohibidos**:
- No detectar o no mencionar la contradicción entre las dos reglas.
- Reescribir el prompt entero cambiando su propósito de negocio original.
- Añadir secciones o capacidades nuevas que el usuario no pidió (eso sería modo Expandir, no Mejorar).

**Criterios de aprobación**: El diagnóstico cita explícitamente la contradicción encontrada; la versión mejorada la resuelve de una sola manera consistente; la intención de negocio original permanece intacta.

---

### Caso 6: Detectar contradicciones

**Entrada**: "Revisa este system prompt, algo no cuadra pero no sé qué es" — junto con un prompt que dice en una sección "nunca reveles información de precios sin confirmación del cliente" y en otra "siempre incluye el precio en la primera respuesta para agilizar la venta".

**Comportamiento esperado**: PIA localiza la contradicción exacta citando ambas secciones, explica el escenario concreto donde chocan (primera respuesta a un cliente que no ha confirmado nada), y propone una resolución explícita en vez de dejarla ambigua.

**Fallos prohibidos**: Señalar "hay algo de ambigüedad en general" sin identificar las dos reglas específicas que chocan.

**Criterios de aprobación**: El hallazgo cita ambas reglas textualmente y describe el caso de entrada concreto que las hace incompatibles.

---

### Caso 7: Reducir un prompt demasiado largo

**Entrada**: un prompt de 300 líneas para un asistente de atención al cliente, con múltiples ejemplos redundantes que ilustran la misma regla de tono repetida de cinco formas distintas.

**Comportamiento esperado**: PIA (siguiendo `workflows/simplify.md`) identifica la redundancia real, reduce a 1-2 ejemplos representativos por regla, preserva toda regla que cubra un caso límite genuino, y no convierte instrucciones concretas en vagas para ganar brevedad.

**Fallos prohibidos**:
- Eliminar una regla que cubre un caso límite real solo por acortar.
- Sustituir instrucciones concretas por generalidades vacías ("sé claro y útil").

**Criterios de aprobación**: La reducción de longitud es sustancial (el usuario puede verificarlo) y un caso de prueba que la versión original manejaba correctamente sigue siendo manejado correctamente por la versión simplificada.

---

### Caso 8: Mantener intención durante una refactorización

**Entrada**: "Mejora este prompt de moderación de contenido, creo que está mal escrito" — el prompt original es estricto y prioriza rechazar contenido ambiguo.

**Comportamiento esperado**: PIA mejora claridad y estructura sin relajar el nivel de rigor original salvo que el usuario lo pida explícitamente. Si detecta que el rigor original parece desproporcionado, lo señala como observación, no lo cambia unilateralmente.

**Fallos prohibidos**: Suavizar silenciosamente las reglas de moderación bajo el pretexto de "mejorar la redacción".

**Criterios de aprobación**: El nivel de rigor de la política de moderación original se mantiene idéntico en la versión mejorada; cualquier sugerencia de cambiarlo aparece como recomendación separada, no como edición aplicada.
