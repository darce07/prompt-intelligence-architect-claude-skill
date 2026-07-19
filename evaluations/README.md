# Evaluaciones de comportamiento

Casos de prueba para verificar que PIA se comporta como se especifica en `SKILL.md` y las referencias. No son pruebas automatizadas ejecutables (PIA no tiene un arnés de test runner) — son casos que un humano (o un revisor con acceso a Claude Code) puede ejecutar manualmente para verificar comportamiento, siguiendo el framework de `references/evaluation-framework.md`, sección 4.

## Cómo está organizado

| Archivo | Cubre |
|---|---|
| `creation-cases.md` | Modo Crear: de necesidad vaga a artefacto completo |
| `improvement-cases.md` | Modo Mejorar: refactorización preservando intención |
| `conversion-cases.md` | Modo Convertir: cambio de formato/plataforma |
| `security-cases.md` | Rechazo de secretos, herramientas destructivas, prompt injection |
| `evolution-cases.md` | Protocolo de aprendizaje gobernado (proponer, no aplicar en silencio) |

## Formato de cada caso

Cada caso sigue la estructura de `references/evaluation-framework.md`, sección 4:

```text
### Caso N: {{nombre}}
**Entrada**: {{lo que el usuario dice}}
**Comportamiento esperado**: {{qué debería hacer PIA, verificable}}
**Fallos prohibidos**: {{comportamientos que invalidan el caso aunque el resultado "parezca" bien}}
**Criterios de aprobación**: {{condición objetiva o criterio de revisión humana}}
```

## Cómo usar estos casos

1. Da la entrada exacta del caso a una sesión de Claude Code con esta skill instalada.
2. Compara el resultado contra "Comportamiento esperado" y verifica que ninguno de los "Fallos prohibidos" ocurrió.
3. Marca el caso como aprobado solo si cumple los "Criterios de aprobación".
4. Si un caso falla de forma repetible, es candidato a convertirse en una lección o antipatrón en `knowledge/` (ver `references/continuous-improvement.md`) y, si afecta comportamiento fundamental, a una entrada en `CHANGELOG.md`.

## Cobertura mínima

Estos archivos cubren los 15 casos mínimos especificados para esta skill: crear desde necesidad vaga, mejorar prompt desordenado, convertir prompt a skill, diseñar agente con herramientas, diseñar sistema multiagente, detectar contradicciones, reducir prompt largo, crear plantilla reusable, diseñar memoria segura, proponer mejora sin aplicarla automáticamente, rechazar guardar credenciales, adaptar a Claude Code, explicar elección de arquitectura, mantener intención en refactorización, diseñar criterios objetivos de evaluación.
