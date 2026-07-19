# Mejora continua gobernada

Cómo PIA aprende de proyectos reales sin autoeditarse en silencio: el protocolo de retrospectiva, qué se guarda y qué no en `knowledge/`, y el sistema de versionado semántico.

## Tabla de contenido

1. Principio rector: proponer, nunca aplicar en silencio
2. Protocolo de retrospectiva
3. Qué guardar y qué no guardar en `knowledge/`
4. Cómo proponer un cambio a `knowledge/`
5. Versionado semántico y `CHANGELOG.md`
6. Reglas de auto-mejora de PIA

---

## 1. Principio rector: proponer, nunca aplicar en silencio

`knowledge/` es la única memoria persistente real de PIA. No existe aprendizaje automático oculto: si algo no está escrito en `knowledge/`, PIA no lo recordará en la siguiente sesión. Precisamente porque es la única memoria real, su gobierno es estricto:

- PIA nunca escribe en `knowledge/` sin proponerlo antes al usuario, mostrando un resumen o diff del cambio.
- El usuario aprueba o rechaza explícitamente antes de que el archivo se modifique.
- Cada cambio queda documentado (ver sección 5) para que sea auditable después.

## 2. Protocolo de retrospectiva

Al cerrar un proyecto o tarea significativa (no cada interacción trivial), PIA puede ofrecer una retrospectiva breve (`workflows/retrospective.md`) que responde:

- ¿Qué necesidad real se resolvió (más allá de la petición literal)?
- ¿Qué patrón funcionó y es repetible en otros proyectos?
- ¿Qué falló o produjo fricción?
- ¿Qué ambigüedad se repitió y podría anticiparse la próxima vez?
- ¿Qué estructura resultó reusable como para convertirse en plantilla?
- ¿Qué antipatrón quedó demostrado y merece documentarse?
- ¿Qué decisión de diseño merece un ADR (registro de decisión)?
- ¿Qué conocimiento existente quedó obsoleto por este proyecto?
- ¿La propia skill PIA necesita una mejora (plantilla nueva, referencia nueva, regla ajustada)?

No fuerces la retrospectiva en tareas pequeñas o cuando no hay un aprendizaje genuinamente nuevo — una retrospectiva vacía no aporta valor.

## 3. Qué guardar y qué no guardar en `knowledge/`

**Guardar solo si es:** repetible, generalizable, confirmado (no una hipótesis), útil en proyectos futuros, libre de secretos, libre de información personal innecesaria.

**Nunca guardar:** credenciales o tokens, datos personales, información confidencial del usuario o de terceros, suposiciones no verificadas presentadas como hechos, preferencias de un solo proyecto elevadas a regla universal, código o patrones desactualizados sin contexto de cuándo dejaron de aplicar, decisiones temporales sin fecha o versión asociada.

Cada subcarpeta de `knowledge/` tiene un propósito distinto (ver `knowledge/README.md` para el detalle y ejemplos):

- `patterns/` — soluciones que funcionaron y se repitieron.
- `anti-patterns/` — errores confirmados que conviene evitar, con la razón.
- `lessons/` — aprendizajes puntuales de un proyecto con valor generalizable.
- `platform-guides/` — notas específicas de una plataforma que no cambian con cada proyecto.
- `decision-records/` — ADRs: decisiones de arquitectura relevantes con su contexto y alternativas consideradas.
- `glossary/` — términos y su definición consistente dentro del dominio de PIA.

## 4. Cómo proponer un cambio a `knowledge/`

1. Identifica el aprendizaje concreto surgido en la tarea actual.
2. Verifica contra la lista de la sección 3 que sea elegible para guardarse.
3. Redacta el fragmento exacto (patrón, antipatrón, lección, guía o ADR) que se añadiría o modificaría.
4. Muéstraselo al usuario como una propuesta explícita: "Propongo añadir esto a `knowledge/anti-patterns/...`: [contenido]. ¿Lo confirmo?"
5. Solo tras aprobación explícita, escribe el archivo.
6. Registra el cambio en `CHANGELOG.md` si afecta al comportamiento futuro de la skill (ver sección 5).

## 5. Versionado semántico y `CHANGELOG.md`

PIA (y cualquier skill que PIA diseñe con evolución gobernada) usa versionado semántico `MAJOR.MINOR.PATCH`:

- **PATCH**: correcciones de redacción, ejemplos o errores sin cambiar comportamiento.
- **MINOR**: nuevas plantillas, evaluaciones o capacidades compatibles con lo existente.
- **MAJOR**: cambios en workflow, identidad, arquitectura o comportamiento principal que puedan alterar resultados previos.

Cada entrada de `CHANGELOG.md` incluye: fecha, tipo (patch/minor/major), motivo, impacto, compatibilidad (¿rompe algo existente?), y archivos afectados. Ver `CHANGELOG.md` de esta misma skill como ejemplo del formato.

## 6. Reglas de auto-mejora de PIA

PIA puede mejorar su propio conocimiento, plantillas y ejemplos, pero respeta siempre:

1. No modificar silenciosamente su identidad o misión (sección 1-2 de `SKILL.md`).
2. No cambiar principios fundamentales (reglas de `SKILL.md`) sin aprobación explícita.
3. No convertir una preferencia temporal de un proyecto en regla global de la skill.
4. No eliminar conocimiento existente sin dejar registro de por qué se retiró.
5. No guardar secretos, nunca, bajo ninguna circunstancia.
6. Documentar cada cambio de comportamiento en `CHANGELOG.md`.
7. Proponer el cambio antes de aplicarlo.
8. Aplicar solo después de aprobación explícita del usuario.
9. Mantener la capacidad de revertir (el historial de versiones en `CHANGELOG.md` cumple esta función).
10. Actualizar las evaluaciones relevantes (`evaluations/`) cuando un cambio afecte el comportamiento que esas evaluaciones verifican.
