# Workflow: Plantillizar

Cuándo usarlo: el usuario tiene una solución específica que funcionó y quiere convertirla en algo reutilizable para casos futuros similares — "convierte esto en una plantilla que pueda reutilizar".

## Pasos

1. **Lee la solución concreta completa** e identifica qué partes son específicas del caso puntual (nombres propios, datos concretos, decisiones que solo aplicaban a esa situación) frente a qué partes son la estructura genuinamente reutilizable.

2. **Extrae las variables.** Todo lo específico del caso se convierte en un placeholder claramente marcado (`{{nombre_variable}}` o similar), con una nota de qué se espera ahí.

3. **Preserva la estructura que hizo funcionar la solución original** — el orden de las secciones, las reglas de decisión, el formato de salida. Esa es la parte valiosa que se está capturando.

4. **Generaliza sin perder utilidad.** Una plantilla demasiado genérica (todo convertido en placeholder, sin ninguna guía concreta) es tan inútil como la solución hiper-específica que reemplaza. Deja ejemplos de valores típicos para las variables clave.

5. **Documenta cómo usar la plantilla**: qué variables hay que rellenar, cuáles son opcionales, qué partes normalmente no hace falta tocar.

6. **Si la plantilla es de un tipo cubierto por `templates/`**, evalúa si conviene proponerla como adición a esa carpeta (ver protocolo de propuesta en `references/continuous-improvement.md`) en vez de solo entregarla al usuario.

## Formato de respuesta

```text
Qué se generalizó y qué se dejó fijo   — la línea entre variable y estructura
Plantilla                                 — el artefacto con placeholders claramente marcados
Guía de uso                                — qué rellenar, con ejemplos de valores típicos
Caso de origen (referencia)                  — de qué solución concreta se extrajo, para trazabilidad
```

## Fallos prohibidos en este workflow

- Convertir en placeholder algo que en realidad era una decisión de diseño reutilizable (por ejemplo, una regla de seguridad que debería aplicar siempre, no variar por caso).
- Entregar una plantilla tan genérica que no da ninguna guía real de qué poner en cada variable.
- No declarar de qué caso concreto se extrajo la plantilla.
