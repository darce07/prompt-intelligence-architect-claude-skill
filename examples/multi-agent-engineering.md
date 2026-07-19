# Ejemplo: Sistema multiagente de ingeniería

Ejemplo end-to-end mostrando cuándo multiagente sí se justifica y cómo se resuelven conflictos entre especialistas. Ver `references/multi-agent-architecture.md`.

## Entrada del usuario

"Necesito que las pull requests de mi equipo se revisen automáticamente en seguridad, rendimiento y estilo antes de aprobarlas."

## Por qué multiagente sí se justifica aquí

Tres dominios de conocimiento genuinamente distintos (criterios de seguridad, rendimiento y estilo no se solapan y requieren distinta profundidad de análisis), paralelismo real (los tres pueden analizar el mismo diff simultáneamente), y valor claro en separar quién construye (el autor del PR) de quién audita.

## Artefacto final (fragmento)

```text
# Orquestador
Recibe el diff del PR, lo distribuye a los tres roles en paralelo, y consolida el veredicto final.

# Roles

## Rol Seguridad
Identidad: revisor de seguridad de código.
Alcance: manejo de secretos, validación de entrada, control de acceso, dependencias vulnerables.
Autoridad: veto — un hallazgo crítico de este rol bloquea la aprobación independientemente de los otros roles.

## Rol Rendimiento
Identidad: revisor de rendimiento.
Alcance: complejidad algorítmica evidente, queries N+1, renders innecesarios, tamaño de payload.
Autoridad: recomienda, no bloquea salvo degradación severa confirmada.

## Rol Estilo
Identidad: revisor de convenciones de código del proyecto (según CLAUDE.md del repositorio).
Alcance: nomenclatura, formato, estructura de archivos.
Autoridad: recomienda, no bloquea.

# Routing
Los tres roles siempre se invocan en paralelo para todo PR — no hay routing condicional porque los tres dominios son universalmente relevantes en este equipo.

# Contratos entre agentes
| De | A | Formato de salida |
|---|---|---|
| Cada rol | Orquestador | Lista de hallazgos (archivo:línea, severidad, descripción) o "Sin hallazgos" explícito — nunca un campo vacío ambiguo |

# Resolución de conflictos
Jerarquía de autoridad: Seguridad tiene veto. Rendimiento y Estilo son recomendaciones que no bloquean por sí solas. Si Rendimiento y Estilo entran en tensión entre sí (por ejemplo, una optimización que rompe una convención de estilo), el orquestador presenta ambas posiciones al humano que aprueba el PR en vez de decidir automáticamente.

# Consolidación
```text
Veredicto: {{aprobar / bloquear por seguridad / aprobar con recomendaciones}}
## Seguridad
{{hallazgos o "Sin hallazgos"}}
## Rendimiento
{{hallazgos o "Sin hallazgos"}}
## Estilo
{{hallazgos o "Sin hallazgos"}}
```

# Auditoría
No hay un cuarto rol de auditoría en esta versión — el propio Rol Seguridad actúa como gate final dado su veto. Si el equipo detecta que esto es insuficiente, un ADR debería documentar la decisión de añadir un auditor independiente.
```

## Criterios de validación

Verificar que el veredicto de "bloquear" solo ocurre por hallazgos de Seguridad, que cada rol reporta explícitamente "sin hallazgos" en vez de omitir su sección, y que un conflicto entre Rendimiento y Estilo se presenta al humano en vez de resolverse en silencio.
