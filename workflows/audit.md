# Workflow: Auditar

Cuándo usarlo: el usuario pide una evaluación de calidad, seguridad o consistencia de instrucciones existentes, sin pedir necesariamente que se corrijan — "audita estas instrucciones", "revisa esto antes de publicarlo".

## Pasos

1. **Lee el artefacto completo.**

2. **Aplica los 10 quality gates** de `references/evaluation-framework.md` uno por uno. Cada gate que falle es un hallazgo con ubicación concreta en el texto (cita la línea o sección).

3. **Aplica el checklist de seguridad** de `references/security-and-privacy.md` sin excepción, incluso si el usuario no mencionó seguridad explícitamente — es responsabilidad de PIA señalarlo.

4. **Aplica las 6 perspectivas de crítica** de `references/evaluation-framework.md` para encontrar fallos que los gates por sí solos no capturan (por ejemplo, problemas de mantenibilidad futura).

5. **Clasifica cada hallazgo por severidad:**
   - **Crítico**: rompe la funcionalidad, expone un riesgo de seguridad, o produce comportamiento peligroso/incorrecto en casos previsibles.
   - **Importante**: degrada calidad, mantenibilidad o consistencia mtoo, pero no es peligroso.
   - **Menor**: mejora posible sin urgencia.

6. **Reconoce fortalezas reales**, no como cortesía sino porque informan qué preservar si luego se pide una corrección.

7. **Si el usuario pidió corrección**, entrega también la versión corregida (equivalente al workflow Mejorar) después del veredicto.

## Formato de respuesta

```text
Veredicto              — resumen de 2-3 líneas: ¿listo para usar, listo con reservas, o no listo?
Hallazgos críticos       — cada uno con ubicación, por qué es crítico, y el gate/criterio que viola
Hallazgos importantes     — igual formato, severidad menor
Fortalezas                 — qué está genuinamente bien hecho
Recomendaciones              — próximos pasos concretos, priorizados
Versión corregida             — solo si el usuario la pidió explícitamente
```

## Fallos prohibidos en este workflow

- Dar un veredicto positivo genérico sin evidencia concreta de haber aplicado los gates.
- Mezclar severidades (tratar un hallazgo menor como si bloqueara el uso, o un hallazgo crítico como nota al pie).
- Omitir el checklist de seguridad porque el usuario no lo pidió explícitamente.
- Corregir el artefacto sin que se haya pedido, cuando el usuario solo quería el veredicto.
