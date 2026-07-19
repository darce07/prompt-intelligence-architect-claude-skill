# Framework de evaluación

Cómo PIA critica sus propios artefactos antes de entregarlos (Fase 6 de `references/prompt-architecture.md`), los 10 criterios de calidad, los 10 quality gates, y cómo diseñar evaluaciones para artefactos que otros van a mantener.

## Tabla de contenido

1. Las 6 perspectivas de crítica
2. Los 10 criterios de calidad (puntuación 0-5)
3. Los 10 quality gates
4. Cómo diseñar evaluaciones de comportamiento
5. Evaluación objetiva vs. subjetiva

---

## 1. Las 6 perspectivas de crítica

Antes de entregar cualquier artefacto, revísalo desde estas seis perspectivas, buscando **fallos concretos**, no observaciones genéricas:

1. **Arquitecto**: ¿la estructura elegida (monolítica/modular, roles, flujo) es la adecuada para el tamaño real del problema? ¿Sobra o falta estructura?
2. **Usuario final**: ¿alguien que reciba este artefacto por primera vez puede usarlo sin contexto adicional que no se le dio?
3. **Especialista de dominio**: ¿el contenido es correcto y suficiente para el dominio específico (seguridad, frontend, datos, etc.) que el artefacto cubre?
4. **Crítico adversarial**: ¿qué entrada razonable rompe este artefacto? ¿Dónde hay ambigüedad, contradicción o instrucción imposible?
5. **Mantenedor futuro**: si alguien (humano o IA) tiene que modificar esto en seis meses sin memoria de por qué se diseñó así, ¿puede hacerlo sin reescribirlo por completo?
6. **Evaluador de calidad**: ¿existen criterios verificables de que el artefacto cumple su propósito, o el éxito es puramente subjetivo sin forma de comprobarlo?

Un hallazgo válido de esta revisión se ve como: "la regla de la sección 3 contradice el límite declarado en la sección 5 cuando el usuario pide X" — no como "podría ser más claro".

## 2. Los 10 criterios de calidad (puntuación 0-5)

Evalúa el artefacto en cada uno, de 0 (ausente) a 5 (ejemplar):

1. **Claridad** — ¿las instrucciones son inequívocas?
2. **Cobertura** — ¿cubre los casos relevantes del dominio, incluyendo los límite?
3. **Coherencia** — ¿ninguna regla contradice a otra?
4. **Modularidad** — ¿está dividido en piezas con responsabilidad única cuando el tamaño lo justifica?
5. **Mantenibilidad** — ¿se puede modificar una parte sin romper el resto?
6. **Reutilización** — ¿puede aplicarse a más de un caso concreto, o está sobreajustado a un solo ejemplo?
7. **Adaptabilidad** — ¿se ajusta razonablemente si cambian entradas, plataforma o escala?
8. **Seguridad** — ¿cumple `references/security-and-privacy.md`?
9. **Verificabilidad** — ¿existe forma de comprobar si el artefacto funciona como se espera?
10. **Utilidad práctica** — ¿resuelve la necesidad real del usuario, no solo la petición literal?

Un artefacto no debe entregarse como definitivo si tiene una debilidad crítica conocida (puntuación 0-1 en cualquier criterio) sin advertirla explícitamente al usuario.

## 3. Los 10 quality gates

Antes de la entrega (Fase 8), verifica que el artefacto pase cada gate. Un "no" en cualquiera exige volver a la Fase 7 (refactorización) o advertir explícitamente la limitación:

| Gate | Pregunta |
|---|---|
| 1 — Intención | ¿El artefacto resuelve la necesidad real, no solo la petición literal? |
| 2 — Contexto | ¿Incluye el contexto necesario sin depender de conocimiento implícito no garantizado? |
| 3 — Comportamiento | ¿Las reglas guían claramente las decisiones, incluso en casos límite? |
| 4 — Formato | ¿La salida esperada está definida de forma concreta? |
| 5 — Fallos | ¿Se contemplan ambigüedad, datos faltantes y errores de herramientas? |
| 6 — Herramientas | ¿Las herramientas están descritas sin inventar capacidades no confirmadas? |
| 7 — Mantenibilidad | ¿Puede modificarse una parte sin reescribirlo por completo? |
| 8 — Evaluación | ¿Puede verificarse objetiva o subjetivamente si funciona? |
| 9 — Seguridad | ¿Evita filtraciones, acciones peligrosas y manejo incorrecto de secretos? |
| 10 — Evolución | ¿Puede aprender/actualizarse sin degradar su comportamiento existente? |

## 4. Cómo diseñar evaluaciones de comportamiento

Cada evaluación (ver `evaluations/` para el formato completo) debe incluir cuatro partes:

- **Entrada**: la petición o escenario concreto que se le da al artefacto.
- **Comportamiento esperado**: qué debería hacer, en términos verificables.
- **Fallos prohibidos**: comportamientos que, si ocurren, hacen fallar la evaluación aunque el resultado "parezca" bien (por ejemplo: "no debe guardar la credencial", "no debe inventar una API que no existe").
- **Criterios de aprobación**: la condición objetiva (o el criterio de revisión humana, si es subjetivo) que determina si la evaluación pasa.

Una evaluación sin "fallos prohibidos" solo mide si el artefacto hizo *algo* razonable, no si evitó los errores que de verdad importan.

## 5. Evaluación objetiva vs. subjetiva

- **Objetiva**: el resultado se puede comprobar mecánicamente (¿el JSON tiene el campo requerido?, ¿el prompt rechazó guardar la credencial?, ¿la skill generada tiene las carpetas requeridas?). Prefiere este tipo siempre que el artefacto lo permita.
- **Subjetiva**: requiere juicio humano (¿el tono es adecuado?, ¿la explicación es clara para un principiante?). No fuerces una evaluación subjetiva a parecer objetiva con una métrica falsa — declárala como revisión humana y da el criterio que el revisor debe aplicar.

La mayoría de los artefactos de PIA combinan ambas: gates de seguridad y estructura son objetivos; calidad de tono y utilidad práctica suelen requerir revisión humana.
