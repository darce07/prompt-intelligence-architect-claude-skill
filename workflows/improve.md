# Workflow: Mejorar

Cuándo usarlo: el usuario ya tiene un prompt, agente o skill y pide que se refactorice, se corrija, o se le dé más calidad — sin querer cambiar su intención de fondo. Incluye el caso "este prompt me da resultados inconsistentes, ayúdame a diagnosticarlo".

## Pasos

1. **Lee el artefacto original completo** antes de proponer cualquier cambio. No mejores a partir de un resumen mental — lee el texto exacto.

2. **Identifica la intención original.** ¿Qué intentaba lograr el autor? Esto se preserva salvo que el usuario pida explícitamente cambiarlo (eso sería modo Expandir o modo Crear desde cero).

3. **Diagnostica usando `references/evaluation-framework.md`.** Aplica los 10 criterios de calidad y busca específicamente:
   - Ambigüedad que explique resultados inconsistentes.
   - Contradicciones entre reglas.
   - Redundancia (misma regla repetida con distinta redacción).
   - Falta de casos límite.
   - Instrucciones que dependen de capacidades no confirmadas.

4. **Prioriza los hallazgos.** No cambies todo lo que "podría" mejorarse — cambia lo que de verdad está causando el problema o afecta materialmente la calidad. Un cambio cosmético sin justificación es ruido para quien tiene que revisar el diff.

5. **Refactoriza preservando la intención.** Si una regla existente parece arbitraria, no la borres sin entender por qué se puso ahí — si no hay forma de saberlo, señálalo como pregunta en vez de eliminarla en silencio.

6. **Verifica compatibilidad.** ¿El cambio rompe algo que dependía del comportamiento anterior (otros prompts que lo invocan, un formato de salida que otro sistema consume)? Decláralo explícitamente.

## Formato de respuesta

```text
Problemas detectados     — lista concreta, cada uno con evidencia del texto original
Cambios principales        — qué se cambió y por qué, no una lista exhaustiva de diffs triviales
Versión mejorada             — el artefacto completo actualizado
Notas de compatibilidad        — qué podría romperse para quien ya usaba la versión anterior
```

## Diagnóstico de inconsistencia (caso especial)

Cuando el usuario reporta "esto me da resultados inconsistentes" sin pedir una reescritura completa, prioriza el diagnóstico sobre la reescritura:

1. Busca instrucciones que dejan una decisión importante sin criterio (el modelo "adivina" distinto cada vez).
2. Busca reglas que compiten entre sí en ciertos casos de entrada.
3. Busca falta de ejemplos donde el formato de salida es ambiguo en prosa pero no en un ejemplo concreto.
4. Propón el cambio mínimo que resuelve la causa raíz, no una reescritura completa, salvo que el usuario la pida.

## Fallos prohibidos en este workflow

- Cambiar la intención original sin que el usuario lo haya pedido.
- Reescribir todo el artefacto cuando el problema real era una sola regla ambigua.
- Eliminar una regla existente sin entender ni señalar por qué estaba ahí.
- No mencionar cuando un cambio puede romper compatibilidad con algo externo.
