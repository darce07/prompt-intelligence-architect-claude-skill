# Plantilla: Prompt simple

Para una tarea puntual sin identidad persistente ni memoria. Ver `references/prompt-architecture.md`, sección 3.

## Cuándo usar esta plantilla

Cuando la tarea es un solo intercambio, no requiere herramientas complejas ni estado entre turnos, y el usuario necesita un resultado concreto y verificable.

## Plantilla

```text
# Objetivo
{{Qué debe lograr esta ejecución, en una frase}}

# Contexto
{{Información necesaria que el modelo no puede inferir por sí solo:
datos del dominio, restricciones del proyecto, audiencia}}

# Rol
{{Perspectiva desde la que debe responder, solo si aporta valor real
— omite esta sección si "actúa como X" no cambia la calidad de la respuesta}}

# Tarea
{{Instrucción concreta y accionable. Usa verbos de acción.
Si hay varios pasos, numéralos.}}

# Reglas
- {{Restricción 1, con la razón si no es obvia}}
- {{Restricción 2}}
- {{Qué NO debe hacer, si es un error previsible}}

# Formato de salida
{{Estructura exacta esperada. Si es posible, muestra el esqueleto
literal que debe seguir la respuesta.}}

# Criterios de calidad
- {{Cómo se sabe que la respuesta es buena, de forma verificable}}
- {{Qué la haría fallar}}
```

## Ejemplo relleno

**Entrada del usuario:** "Necesito un prompt para resumir artículos de noticias en 3 bullets para un boletín interno."

```text
# Objetivo
Resumir un artículo de noticias en 3 bullets accionables para un boletín interno de empresa.

# Contexto
El boletín lo leen empleados no técnicos en menos de 2 minutos. El tono debe ser neutral, sin opinión editorial.

# Tarea
Dado el texto completo de un artículo, produce exactamente 3 bullets que capturen: (1) qué pasó, (2) por qué importa para la empresa, (3) qué acción o seguimiento se espera, si lo hay.

# Reglas
- No incluyas opiniones ni valoraciones que no estén en el artículo original.
- Si el artículo no menciona una acción de seguimiento, el tercer bullet debe decir "Sin acción de seguimiento identificada" en vez de inventar una.
- Máximo 25 palabras por bullet.

# Formato de salida
- {{bullet 1}}
- {{bullet 2}}
- {{bullet 3}}

# Criterios de calidad
- Cada bullet es verificable contra el texto original (no añade información que no esté ahí).
- El tercer bullet nunca inventa una acción inexistente.
```

## Notas de uso

Si la tarea empieza a necesitar memoria entre ejecuciones o manejo de errores de herramientas, esta plantilla ya no es suficiente — pasa a `templates/system-prompt.md` o `templates/agent.md` según corresponda.
