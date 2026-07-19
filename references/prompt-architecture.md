# Arquitectura de prompts

Referencia central de PIA: el flujo de 9 fases que gobierna cualquier tarea, y la anatomía de un prompt simple o system prompt. Otras referencias (agente, skill, multiagente) asumen que ya conoces esto.

## Tabla de contenido

1. Las 9 fases del flujo de trabajo
2. Estrategia de preguntas
3. Anatomía de un prompt simple
4. Anatomía de un system/developer prompt
5. Errores comunes y cómo evitarlos

---

## 1. Las 9 fases del flujo de trabajo

Este es el proceso completo. **Escálalo al tamaño de la tarea**: un prompt de una línea puede recorrer las 9 fases en un párrafo mental; un sistema multiagente las necesita explícitas.

### Fase 1 — Descubrimiento

Determina, sin sobrepreguntar:

- Qué quiere conseguir realmente el usuario (no solo lo que escribió literalmente).
- Quién usará el artefacto (el propio usuario, su equipo, usuarios finales de un producto).
- En qué plataforma funcionará.
- Qué entrada recibirá y qué salida debe producir.
- Qué decisiones debe tomar el modelo.
- Qué restricciones existen (tono, longitud, cumplimiento, dominio).
- Qué información falta que sea crítica.
- Qué herramientas puede utilizar.
- Qué riesgos deben evitarse.
- Qué nivel de autonomía tendrá.
- Si necesita memoria, acceso a archivos, o actuar dentro de un repositorio.
- Si debe colaborar con otras skills o agentes.

Infiere cuando la inferencia sea razonable y reversible; pregunta cuando no lo sea (ver sección 2).

### Fase 2 — Clasificación

Clasifica el artefacto solicitado antes de diseñar: prompt simple, system prompt, developer prompt, plantilla, agente, skill, multiagente, workflow, RAG, tool-using agent, evaluador, crítico/revisor, `CLAUDE.md`, reglas de repositorio, biblioteca de prompts, o especificación técnica. La clasificación determina qué referencia y plantilla usar (ver tabla en `SKILL.md`).

### Fase 3 — Arquitectura

Decide antes de escribir texto: estructura monolítica o modular, archivos necesarios, roles, responsabilidades, flujo de trabajo, entradas/salidas, herramientas, memoria, persistencia, evaluaciones, quality gates, mecanismos de fallback, versionado, compatibilidad futura.

### Fase 4 — Diseño conductual

Define explícitamente: identidad, misión, prioridades, límites, forma de razonar observable, reglas de decisión, prohibiciones, manejo de ambigüedad, manejo de errores, tono, profundidad, formato de respuesta, criterios de escalamiento (cuándo el modelo debe detenerse y preguntar en vez de asumir).

### Fase 5 — Construcción

Construye el artefacto con estructura clara y directamente utilizable. Usa la plantilla correspondiente de `templates/` como esqueleto, no como resultado final — adáptala siempre al caso concreto.

### Fase 6 — Crítica adversarial

Antes de considerar el borrador terminado, evalúalo buscando: ambigüedad, contradicciones, instrucciones imposibles de cumplir, redundancia, sobreajuste a un solo ejemplo, dependencias ocultas (asume herramientas o contexto no garantizado), falta de casos límite, riesgos de seguridad, falta de criterios de calidad verificables, dificultad de mantenimiento, exceso de longitud, falta de ejemplos, activaciones accidentales (para skills), supuestos no declarados. Ver `references/evaluation-framework.md` para el detalle de las 6 perspectivas de crítica.

### Fase 7 — Refactorización

Corrige lo que la crítica encontró. No apliques cambios cosméticos que no resuelvan un hallazgo real.

### Fase 8 — Entrega

Entrega, en este orden: (1) artefacto final, (2) instrucciones de uso, (3) archivos o estructura si aplica, (4) supuestos relevantes que hiciste, (5) opcionalmente, criterios de prueba. No añadas teoría innecesaria si el usuario solo pidió el entregable.

### Fase 9 — Aprendizaje

Registra únicamente patrones confirmados y reutilizables — nunca datos personales, secretos, credenciales o información sensible. Sigue el protocolo de `references/continuous-improvement.md`: propone, nunca escribe en silencio.

---

## 2. Estrategia de preguntas

Evita los dos extremos: preguntar demasiado (bloquea el avance) y asumir demasiado (produce un resultado incorrecto).

**Pregunta cuando falte información crítica sobre:** plataforma de destino, usuario objetivo, resultado esperado, herramientas disponibles, nivel de autonomía, restricciones regulatorias o institucionales, formato obligatorio, fuente de conocimiento, riesgos importantes, alcance del proyecto.

**No preguntes cuando:** la petición ya sea suficientemente clara, exista una opción estándar segura, la decisión pueda declararse como supuesto explícito en la entrega, la pregunta no cambiaría materialmente el resultado, o el usuario pidió explícitamente una primera versión.

Cuando preguntes, agrupa las preguntas en una sola ronda y limítate a las que de verdad importan — no interrogues por partes.

---

## 3. Anatomía de un prompt simple

Un prompt simple resuelve una tarea puntual, sin necesidad de identidad persistente ni memoria. Estructura mínima (ver `templates/simple-prompt.md`):

```text
Objetivo             — qué debe lograr esta ejecución, en una frase
Contexto              — información necesaria que el modelo no puede inferir
Rol                   — perspectiva desde la que debe responder (si aporta valor)
Tarea                 — instrucción concreta y accionable
Reglas                — restricciones y comportamientos obligatorios
Formato de salida     — estructura exacta esperada
Criterios de calidad  — cómo se sabe que la respuesta es buena
```

Un prompt simple que solo dice "Actúa como experto en X y haz Y" no es una arquitectura: le faltan alcance, formato y criterios de calidad. Ver antipatrón en `knowledge/anti-patterns/`.

## 4. Anatomía de un system/developer prompt

A diferencia del prompt simple, un system/developer prompt define comportamiento persistente a través de múltiples turnos o ejecuciones. Añade a la estructura anterior:

- **Identidad estable**: quién es el asistente en este contexto, sin cambiar entre turnos.
- **Manejo de ambigüedad**: qué hacer cuando la petición del usuario sea incompleta.
- **Manejo de errores**: qué hacer cuando una herramienta falla o el resultado es incierto.
- **Límites explícitos**: qué el asistente no debe hacer, y qué debe hacer en su lugar (no basta con prohibir; hay que indicar la alternativa).
- **Criterios de escalamiento**: cuándo debe detenerse a preguntar en vez de continuar.

Un system prompt bien diseñado no repite la misma regla en varios lugares con distinta redacción (redundancia) ni exige comportamientos contradictorios entre secciones. Antes de entregarlo, verifica que dos reglas cualesquiera no puedan chocar en un caso real.

---

## 5. Errores comunes y cómo evitarlos

| Error | Por qué falla | Cómo evitarlo |
|---|---|---|
| Prompt genérico ("actúa como experto en X") | No define alcance, entradas, salida ni criterios de calidad | Usa la anatomía completa de la sección 3 |
| Repetir la petición del usuario con otras palabras | No añade valor arquitectónico | Aplica las 9 fases; el valor está en el diseño, no en la paráfrasis |
| Reglas absolutas sin excepciones | Rompe en el primer caso límite real | Declara la regla y su excepción conocida, o el criterio para decidir |
| Mezclar instrucciones con conocimiento de referencia | Infla el prompt principal y dificulta el mantenimiento | Separa: instrucciones en el prompt, conocimiento en archivos de referencia cargados bajo demanda |
| Prometer aprendizaje automático sin persistencia real | Genera expectativas falsas sobre el sistema | Sé explícito: solo hay memoria si hay almacenamiento real (archivo, base de datos, etc.) |
