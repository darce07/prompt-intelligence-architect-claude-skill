# Arquitectura multiagente

Cómo diseñar un sistema con más de un agente: cuándo se justifica, cómo definir roles y contratos entre agentes, y cómo evitar la complejidad innecesaria.

## Tabla de contenido

1. Cuándo un sistema multiagente se justifica (y cuándo no)
2. Componentes obligatorios
3. Contratos entre agentes
4. Resolución de conflictos y consolidación
5. Auditoría del sistema completo

---

## 1. Cuándo un sistema multiagente se justifica

Un sistema multiagente añade coordinación, latencia y superficie de fallo. Se justifica solo cuando:

- La tarea requiere **conocimientos de dominio genuinamente distintos** que no conviene mezclar en un solo prompt (por ejemplo, seguridad, frontend y datos con criterios de calidad diferentes).
- Hay **paralelismo real**: partes de la tarea pueden ejecutarse de forma independiente y luego consolidarse.
- Se necesita un **rol de auditoría o crítica independiente** del rol que produce el trabajo (separación entre quien construye y quien revisa).

**No se justifica** cuando un solo agente bien diseñado, con las secciones adecuadas, puede cubrir el alcance. "Proponer multiagentes cuando uno es suficiente" es un antipatrón explícito (ver `knowledge/anti-patterns/`) — añade orquestación, rutas de fallo y coste sin beneficio real.

## 2. Componentes obligatorios

Todo sistema multiagente (ver `templates/multi-agent.md`) debe definir:

- **Orquestador**: quién recibe la petición original, decide qué roles intervienen y en qué orden, y consolida el resultado final. Puede ser un agente explícito o un flujo declarado.
- **Roles**: cada agente especialista, con su identidad, misión y alcance definidos como en `references/agent-architecture.md` — sin solaparse entre sí.
- **Routing**: la lógica que decide qué rol(es) intervienen para una petición dada. Debe ser explícita, no "el orquestador decide con buen juicio" sin más detalle.
- **Contratos entre agentes**: qué formato de entrada espera cada rol y qué formato de salida entrega (sección 3).
- **Flujos**: si los roles se ejecutan en paralelo, en secuencia, o con dependencias parciales.
- **Resolución de conflictos**: qué pasa cuando dos roles producen recomendaciones incompatibles (sección 4).
- **Consolidación**: cómo se combina el trabajo de los roles en una única respuesta coherente para el usuario.
- **Auditoría**: si existe un rol de revisión independiente, y en qué punto del flujo actúa.

## 3. Contratos entre agentes

Cada transición entre agentes es una interfaz y debe tratarse como tal:

- Define el **formato exacto** de lo que un agente entrega al siguiente (estructura, campos obligatorios, qué significa "vacío" o "sin hallazgos").
- Define qué pasa si el agente productor **no puede cumplir el contrato** (por ejemplo, no tiene información suficiente): debe devolver un estado explícito, no inventar contenido para rellenar el formato.
- No asumas que un agente "entenderá" la salida de otro por contexto compartido implícito — dos agentes no comparten memoria salvo que el diseño lo declare explícitamente.

## 4. Resolución de conflictos y consolidación

Cuando dos o más especialistas producen recomendaciones incompatibles, el sistema necesita una regla explícita, no "el orquestador usa su criterio". Opciones habituales, a elegir según el dominio:

- **Jerarquía de autoridad**: un rol (por ejemplo, seguridad) tiene veto sobre otros en su dominio.
- **Escalamiento a humano**: el conflicto se presenta al usuario en vez de resolverse automáticamente, cuando el riesgo de decidir mal es alto.
- **Síntesis explícita**: el orquestador debe declarar ambas posiciones y su resolución, no ocultar el desacuerdo detrás de una única recomendación.

La consolidación final debe ser legible por el usuario como una sola voz coherente — no un collage visible de fragmentos de cada agente, salvo que el formato de salida lo pida así (por ejemplo, un informe con secciones firmadas por especialista).

## 5. Auditoría del sistema completo

Antes de entregar un diseño multiagente, verifica con la crítica adversarial de `references/evaluation-framework.md` además de:

- ¿Cada rol tiene un alcance que no se solapa con otro? (solape = desperdicio y posible contradicción)
- ¿El routing cubre el caso en que ningún rol especializado aplica? (fallback a un rol genérico o a pedir aclaración)
- ¿Qué pasa si un agente falla o no responde? ¿El sistema completo se bloquea o degrada con gracia?
- ¿La latencia acumulada (si hay pasos secuenciales) es aceptable para el caso de uso?
- ¿Existe un punto único de fallo (por ejemplo, el orquestador) sin plan de manejo de errores?
