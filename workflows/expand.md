# Workflow: Expandir

Cuándo usarlo: el usuario pide añadir una capacidad nueva a un artefacto existente sin romper lo que ya funciona — "añade soporte para X", "quiero que también pueda Y".

## Pasos

1. **Lee el artefacto completo** y entiende su arquitectura actual antes de añadir nada — la capacidad nueva debe encajar en la estructura existente, no imponerse sobre ella.

2. **Verifica si la capacidad nueva pertenece realmente a este artefacto** o si merece un artefacto separado (por ejemplo, un rol nuevo en un sistema multiagente en vez de sobrecargar el rol existente). Ver el antipatrón "sobrecargar con roles innecesarios" en `knowledge/anti-patterns/`.

3. **Diseña la extensión con las mismas fases 3-4** de `references/prompt-architecture.md` (arquitectura y diseño conductual), pero acotado a la parte nueva: qué rol/sección la maneja, qué entradas/salidas tiene, qué reglas nuevas introduce, cómo se relaciona con las reglas existentes.

4. **Verifica que no rompe lo existente.** Antes de finalizar, recorre las reglas y ejemplos originales y confirma que siguen siendo válidos con la extensión añadida. Si la nueva capacidad exige cambiar una regla existente, eso ya no es "expandir" sin más — decláralo como un cambio de comportamiento existente (posible MAJOR, ver `references/continuous-improvement.md`).

5. **Actualiza la documentación asociada** (ejemplos, evaluaciones) que la extensión afecte — no dejes ejemplos desactualizados que ya no reflejan el comportamiento real.

## Formato de respuesta

```text
Capacidad añadida            — qué hace la extensión, en concreto
Integración con lo existente   — cómo encaja sin romper el comportamiento anterior
Artefacto actualizado            — el artefacto completo con la extensión incorporada
Verificación de no-regresión       — confirmación explícita de qué comportamiento previo sigue intacto
```

## Fallos prohibidos en este workflow

- Añadir la capacidad de forma que rompe o contradice una regla existente sin advertirlo.
- Sobrecargar un rol o sección existente cuando la capacidad nueva merecía su propio espacio.
- Expandir sin actualizar ejemplos o evaluaciones que quedan desactualizados por el cambio.
