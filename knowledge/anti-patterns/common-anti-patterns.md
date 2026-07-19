# Antipatrones comunes

Origen: derivados de la sección 19 de la especificación fundacional de PIA. Punto de partida sujeto a confirmación con casos reales (ver `references/continuous-improvement.md`).

## Antipatrón: Prompt genérico de rol sin arquitectura

**Qué es**: entregar algo equivalente a "Actúa como experto en X y haz Y" sin alcance, formato de salida, ni criterios de calidad.

**Por qué falla**: no define qué entra, qué sale, ni cómo se sabe si el resultado es bueno — dos ejecuciones pueden producir calidad completamente distinta.

**Cómo evitarlo**: aplicar siempre la anatomía completa de `references/prompt-architecture.md` sección 3, incluso para tareas que parecen simples.

**Visto en**: caso 1 de `evaluations/creation-cases.md`, ejemplo `examples/frontend-reviewer.md`.

---

## Antipatrón: Reglas absolutas sin excepción declarada

**Qué es**: una regla escrita como incondicional ("nunca hagas X") que en la práctica tiene un caso legítimo de excepción no contemplado.

**Por qué falla**: cuando aparece el caso límite real, el modelo debe elegir entre violar la regla o producir un resultado inútil — ambas opciones son peores que haber declarado la excepción de antemano.

**Cómo evitarlo**: para cada regla "nunca/siempre", preguntarse si existe un caso razonable de excepción; si existe, declararlo explícitamente o dar el criterio para decidir en ese caso.

---

## Antipatrón: Sobrecargar con roles innecesarios

**Qué es**: añadir identidad, "personalidad" o roles adicionales a un prompt/agente que no cambian su comportamiento real, solo su superficie retórica.

**Por qué falla**: infla el artefacto sin mejorar el resultado, y dificulta el mantenimiento porque hay más texto que revisar sin beneficio correspondiente.

**Cómo evitarlo**: cada elemento de identidad debe justificar su presencia por el efecto que tiene en el comportamiento, no por sonar más profesional.

---

## Antipatrón: Multiagente cuando un solo agente basta

**Qué es**: dividir una tarea en varios agentes cuando un solo agente bien diseñado, con las secciones adecuadas, cubre el alcance completo.

**Por qué falla**: añade orquestación, contratos entre agentes, latencia y superficie de fallo sin ganancia real — complejidad que hay que mantener sin beneficio correspondiente.

**Cómo evitarlo**: aplicar los criterios de `references/multi-agent-architecture.md` sección 1 antes de diseñar multiagente; si no hay dominios genuinamente distintos, paralelismo real o necesidad de auditoría independiente, usar `templates/agent.md`.

---

## Antipatrón: Prometer aprendizaje automático sin persistencia real

**Qué es**: dar a entender que un agente o skill "aprenderá con el tiempo" o "recordará" sin que exista ningún mecanismo de almacenamiento real detrás de esa promesa.

**Por qué falla**: genera una expectativa falsa en el usuario, que descubre en la práctica que nada persiste entre sesiones.

**Cómo evitarlo**: distinguir explícitamente los tres niveles de memoria de `references/agent-architecture.md` sección 4, y ser explícito sobre cuál aplica en cada artefacto.

---

## Antipatrón: Mezclar instrucciones con conocimiento de referencia

**Qué es**: incluir dentro del prompt/system-prompt principal contenido que en realidad es documentación de consulta ocasional (glosarios extensos, casos de uso detallados, listas de referencia).

**Por qué falla**: infla el artefacto principal, dificulta encontrar las reglas de comportamiento reales entre el ruido, y duplica mantenimiento si el conocimiento cambia.

**Cómo evitarlo**: separar en capas siguiendo el patrón de progressive disclosure (`knowledge/patterns/architecture-patterns.md`) — instrucciones en el artefacto principal, conocimiento en referencias cargadas bajo demanda.

---

## Antipatrón: Autoedición silenciosa de la base de conocimiento

**Qué es**: escribir en `knowledge/` sin proponer el cambio al usuario primero.

**Por qué falla**: rompe la trazabilidad y el control del usuario sobre qué se convierte en "verdad establecida" para futuras sesiones; un aprendizaje mal generalizado puede degradar el comportamiento de la skill silenciosamente.

**Cómo evitarlo**: seguir siempre el protocolo de propuesta-aprobación de `references/continuous-improvement.md` secciones 1 y 4.
