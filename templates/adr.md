# Plantilla: ADR (Architecture Decision Record)

Para documentar una decisión de diseño relevante de un prompt, agente, skill o sistema — de forma que un mantenedor futuro entienda por qué se eligió así y qué alternativas se descartaron. Ver `references/continuous-improvement.md`, sección 3 (`knowledge/decision-records/`).

## Cuándo usar esta plantilla

Cuando una decisión de arquitectura no es obvia por sí sola y merece quedar registrada — por ejemplo, "por qué elegimos un solo agente en vez de multiagente", "por qué esta skill no tiene memoria persistente".

## Plantilla

```text
# ADR-{{número}}: {{título de la decisión}}

Fecha: {{YYYY-MM-DD}}
Estado: {{propuesto / aceptado / reemplazado por ADR-N}}

## Contexto
{{Qué problema o disyuntiva motivó esta decisión. Qué restricciones aplicaban.}}

## Decisión
{{Qué se decidió, en una o dos frases claras.}}

## Alternativas consideradas
- {{alternativa 1}} — descartada porque {{razón}}
- {{alternativa 2}} — descartada porque {{razón}}

## Consecuencias
Positivas:
- {{...}}

Negativas o trade-offs aceptados:
- {{...}}

## Cuándo reconsiderar esta decisión
{{Qué cambio de circunstancias haría válido revisar esto — por ejemplo,
"si el volumen de casos X supera Y" o "si la plataforma añade soporte para Z".}}
```

## Ejemplo relleno

```text
# ADR-003: Sin memoria persistente en el agente de soporte de nivel 1

Fecha: 2026-03-10
Estado: aceptado

## Contexto
El agente de soporte maneja datos de cuenta de clientes. Se evaluó si debía recordar interacciones previas del mismo usuario entre sesiones para dar continuidad.

## Decisión
El agente no tiene memoria persistente entre sesiones; cada conversación empieza sin contexto de interacciones anteriores del mismo usuario, salvo el historial que el sistema de tickets ya provee explícitamente como contexto de entrada.

## Alternativas consideradas
- Memoria persistente por usuario — descartada porque introduce manejo de datos personales que excede el alcance aprobado por privacidad para este agente.

## Cuándo reconsiderar esta decisión
Si el equipo de privacidad aprueba un mecanismo de retención de datos de cliente con las salvaguardas correspondientes.
```

## Notas de uso

Un ADR no es un changelog de cambios de texto — documenta decisiones de arquitectura, no ediciones cosméticas. Para el historial de cambios de comportamiento de una skill, usa `CHANGELOG.md` (ver `references/continuous-improvement.md`, sección 5).
