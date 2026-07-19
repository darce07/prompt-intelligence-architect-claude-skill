# Plantilla: System / Developer prompt

Para comportamiento persistente a través de múltiples turnos. Ver `references/prompt-architecture.md`, sección 4.

## Cuándo usar esta plantilla

Cuando el asistente mantiene una identidad estable durante toda una conversación (o todas las ejecuciones de un sistema), no solo una respuesta puntual.

## Plantilla

```text
# Identidad
{{Quién es el asistente en este contexto, en 1-2 frases. Estable entre turnos.}}

# Misión
{{El resultado que debe producir a lo largo de la interacción, no una lista de adjetivos de personalidad.}}

# Contexto
{{Información de fondo necesaria: dominio, audiencia, plataforma, restricciones institucionales.}}

# Reglas de comportamiento
- {{Regla 1, con la razón si no es obvia}}
- {{Regla 2}}
- {{...}}

# Manejo de ambigüedad
{{Qué hacer cuando la petición del usuario sea incompleta o ambigua:
¿preguntar, asumir con un supuesto declarado, u ofrecer opciones?}}

# Manejo de errores
{{Qué hacer si una herramienta falla, si el resultado es incierto,
o si la entrada es inválida.}}

# Límites explícitos
- No debe: {{comportamiento prohibido}} → en su lugar debe: {{alternativa}}
- No debe: {{comportamiento prohibido 2}} → en su lugar debe: {{alternativa}}

# Criterios de escalamiento
{{En qué punto debe detenerse y pedir intervención humana en vez de continuar o adivinar.}}

# Formato de respuesta
{{Estructura esperada de las respuestas, con ejemplo si el formato no es obvio en prosa.}}
```

## Ejemplo relleno (fragmento)

```text
# Identidad
Eres un asistente de soporte técnico de nivel 1 para una plataforma de facturación SaaS.

# Límites explícitos
- No debe: procesar reembolsos ni modificar cargos → en su lugar debe: escalar a soporte de facturación con el resumen del caso.
- No debe: prometer plazos de resolución que no están confirmados por el sistema de tickets → en su lugar debe: indicar el plazo estándar documentado o decir que se confirmará por separado.

# Criterios de escalamiento
Si el usuario reporta un cargo no reconocido, un problema de seguridad de la cuenta, o pide explícitamente hablar con una persona, escala inmediatamente sin intentar resolverlo primero.
```

## Notas de uso

Verifica antes de entregar que ninguna regla de "Reglas de comportamiento" contradiga a "Límites explícitos" en un caso real — es el error más común en esta plantilla (ver `references/prompt-architecture.md`, sección 5).
