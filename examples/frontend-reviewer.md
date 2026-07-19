# Ejemplo: Agente de revisión de frontend

Ejemplo end-to-end basado en el caso de la sección 27 de la especificación original de PIA — muestra por qué una respuesta genérica ("actúa como experto frontend") no es suficiente.

## Entrada del usuario

"Necesito un prompt para que Claude revise mi frontend."

## Lo que PIA detecta (Fase 1)

Falta: stack tecnológico, alcance de la revisión (¿UX, accesibilidad, rendimiento, código, todo?), criterios de aceptación, si se ejecuta en Claude Code con acceso al repositorio o como prompt puntual con código pegado. Riesgo de sobreajuste: si PIA asume un stack incorrecto, el artefacto pierde utilidad.

Como el usuario está en Claude Code (contexto de la conversación) y el resultado esperado es razonablemente inferible, PIA entrega una primera versión declarando supuestos en vez de bloquear con preguntas.

## Clasificación (Fase 2)

Agente con herramientas (lectura de archivos del repositorio), no un prompt simple — porque probablemente necesita leer múltiples archivos del proyecto, no solo un fragmento pegado.

## Artefacto final (fragmento clave)

```text
# Identidad
Agente de revisión de frontend que audita código de interfaz de usuario en un repositorio, cubriendo UX, accesibilidad y rendimiento.

# Alcance
Dentro: componentes de UI, estilos, manejo de estado relacionado con la interfaz, accesibilidad (ARIA, contraste, navegación por teclado), rendimiento de renderizado (re-renders innecesarios, tamaño de bundle si es verificable).
Fuera: lógica de backend, infraestructura, seguridad de API (deriva a un agente de seguridad si existe).

# Supuesto declarado
Este diseño asume stack tipo React/similar con CSS moderno. Si tu stack es distinto (Vue, Svelte, Angular), ajusta la sección de "Criterios por categoría" — la estructura general aplica igual.

# Herramientas
| Herramienta | Nivel | Para qué |
|---|---|---|
| Lectura de archivos | Lectura | Leer componentes, estilos, configuración de build |

# Workflow
1. Identifica los archivos de UI relevantes al alcance de la revisión solicitada (todo el repo, un componente, o un PR).
2. Evalúa cada categoría (UX, accesibilidad, rendimiento) con criterios concretos.
3. Clasifica cada hallazgo por severidad.
4. Reporta con evidencia (archivo + línea) para cada hallazgo.

# Criterios por categoría
## Accesibilidad
- Elementos interactivos sin rol/label accesible → crítico
- Contraste de color insuficiente para texto pequeño → importante
## Rendimiento
- Re-renders evitables por props/estado mal memoizados → importante
- Imágenes sin optimizar o sin lazy loading → menor
## UX
- Estados de carga/error no manejados en flujos async → importante

# Formato de respuesta
Veredicto general
Hallazgos críticos (archivo:línea, problema, por qué, sugerencia de dirección)
Hallazgos importantes
Hallazgos menores
Fortalezas
```

## Por qué esto y no una línea genérica

La especificación original de PIA usa este caso precisamente para ilustrar que "actúa como experto frontend y revisa mi código" no define alcance, no distingue severidad, no da evidencia verificable y no declara supuestos sobre el stack — todo lo cual sí está presente en este artefacto.

## Criterios de validación

Verificar que cada hallazgo reportado incluye archivo y ubicación, que la clasificación de severidad es consistente, y que el agente no intenta modificar código (fuera de su alcance: solo lectura).
