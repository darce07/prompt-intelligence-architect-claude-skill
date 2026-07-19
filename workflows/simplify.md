# Workflow: Simplificar

Cuándo usarlo: el usuario pide reducir longitud, complejidad o redundancia de un artefacto existente, manteniendo el comportamiento importante — "hazlo más corto", "esto es demasiado prompt para lo que hace".

## Pasos

1. **Lee el artefacto completo** y distingue, regla por regla: qué comportamiento es esencial (el artefacto falla sin ello) frente a qué es explicativo, redundante o cubre un caso que en la práctica nunca ocurre.

2. **Identifica redundancia real**: la misma regla dicha dos veces con distintas palabras, ejemplos que no añaden información nueva, secciones que repiten lo que otra sección ya estableció.

3. **Identifica sobre-especificación**: reglas para casos límite tan improbables que el coste de mantenerlas supera el beneficio, o listas exhaustivas donde un principio general con 2-3 ejemplos bastaría.

4. **Recorta preservando comportamiento verificable.** La prueba de que una simplificación es correcta: si tomas un caso de prueba que el artefacto original manejaba bien, la versión simplificada debe manejarlo igual de bien. Si no puedes garantizar eso para un caso importante, esa regla no se recorta.

5. **No sacrifiques claridad por longitud.** Acortar una frase hasta volverla ambigua no es simplificar, es degradar. El objetivo es la razón señal/ruido, no el conteo de palabras.

6. **Verifica con `references/evaluation-framework.md`** que la versión simplificada sigue pasando los quality gates que la original pasaba.

## Formato de respuesta

```text
Qué se recortó y por qué      — cada recorte con su justificación (redundante / caso improbable / repetido)
Qué se preservó explícitamente  — comportamiento importante que se mantuvo intacto
Versión simplificada              — el artefacto completo
Reducción aproximada                — por ejemplo "de ~180 a ~90 líneas", si es útil para el usuario
```

## Fallos prohibidos en este workflow

- Recortar una regla que cubre un caso límite real solo porque acorta el texto.
- Convertir instrucciones concretas en vagas ("sé claro y útil") para ganar brevedad — eso no es simplificar, es vaciar de contenido.
- Simplificar sin verificar contra los quality gates que la versión anterior superaba.
