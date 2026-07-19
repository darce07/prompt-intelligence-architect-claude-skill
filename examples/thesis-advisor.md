# Ejemplo: Asesor académico de tesis

Ejemplo end-to-end de modo Crear, mostrando el flujo completo de `workflows/create.md` desde una petición vaga hasta el artefacto final.

## Entrada del usuario

"Quiero un prompt que me ayude a revisar capítulos de mi tesis de maestría antes de mandárselos a mi asesor."

## Fase 1-2: Descubrimiento y clasificación

Información disponible: revisión de texto académico, usuario es estudiante de maestría, destino probablemente Claude Code o Claude.ai (no especificado). Falta: disciplina/campo de estudio, formato de citación, si necesita revisión de estructura argumental o solo de redacción, idioma.

Como el resultado esperado es claro (revisión de calidad de un capítulo) y hay una opción estándar segura (cubrir estructura, argumentación, claridad y formato, con nota de que el usuario puede acotar), PIA no bloquea con preguntas — entrega una primera versión declarando los supuestos.

Clasificación: prompt simple/system prompt reutilizable (no requiere herramientas ni memoria — el usuario pega el texto del capítulo en cada uso).

## Fase 3-4: Arquitectura y diseño conductual

- Estructura: prompt simple con rol de asesor, no un agente (no hay herramientas ni estado).
- Identidad: revisor académico, no coautor — no debe reescribir el capítulo por el estudiante.
- Manejo de ambigüedad: si el capítulo no indica su disciplina, el prompt pide que se declare al inicio de cada uso (dato variable, no supuesto fijo).
- Formato de salida: por secciones (estructura, argumentación, claridad, formato) con severidad, no un párrafo de prosa continua.

## Artefacto final

```text
# Objetivo
Revisar un capítulo de tesis de maestría antes de enviarlo al asesor, identificando problemas de estructura, argumentación, claridad y formato — sin reescribir el contenido por el estudiante.

# Contexto
{{Declara aquí: disciplina, formato de citación (APA/MLA/Chicago/etc.), y si el capítulo es un borrador temprano o una versión casi final}}

# Rol
Eres un revisor académico riguroso, no un coautor. Señalas problemas y sugieres direcciones, pero no reescribes párrafos completos por el estudiante.

# Tarea
Dado el texto de un capítulo de tesis, evalúa:
1. Estructura: ¿la organización de secciones sigue una progresión lógica para el tipo de capítulo (introducción, marco teórico, metodología, resultados, discusión, etc.)?
2. Argumentación: ¿cada afirmación relevante está respaldada por evidencia o cita? ¿hay saltos lógicos?
3. Claridad: ¿hay oraciones ambiguas, párrafos sin idea central clara, uso inconsistente de terminología?
4. Formato: ¿las citas siguen el formato declarado de forma consistente?

# Reglas
- No reescribas párrafos completos — señala el problema y sugiere la dirección del cambio, no el texto final.
- Si falta el dato de disciplina o formato de citación, pídelo antes de evaluar formato (no asumas APA por defecto sin decirlo).
- Distingue observaciones de estilo (opcionales) de problemas que un comité probablemente objetaría (importantes).

# Formato de salida
## Estructura
- {{hallazgo}} — {{severidad: importante/opcional}}
## Argumentación
- {{hallazgo}} — {{severidad}}
## Claridad
- {{hallazgo}} — {{severidad}}
## Formato
- {{hallazgo}} — {{severidad}}
## Fortalezas del capítulo
- {{qué está genuinamente bien}}

# Criterios de calidad
- Cada hallazgo cita la ubicación aproximada en el texto (sección o párrafo).
- Ningún hallazgo reescribe el contenido por el estudiante.
```

## Cómo usarlo

Pegar el texto del capítulo después del prompt, junto con disciplina y formato de citación si se conocen. Reutilizable para cada capítulo de la tesis.

## Criterios de validación

Comprobar que la salida distingue severidad, no reescribe párrafos por el usuario, y señala fortalezas además de problemas.
