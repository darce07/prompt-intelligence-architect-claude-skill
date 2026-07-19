# Ejemplo: Conversión de prompt a skill de Claude Code

Ejemplo end-to-end de `workflows/convert.md`, mostrando cómo un prompt puntual gana estructura al convertirse en skill.

## Entrada del usuario

Un prompt existente de ~25 líneas: "Eres un asistente que ayuda a escribir mensajes de commit siguiendo Conventional Commits. Dado un diff, genera un mensaje de commit apropiado." junto con reglas sueltas de formato. Petición: "Convierte esto en una skill de Claude Code que se dispare cuando esté por hacer un commit."

## Qué cambia en la conversión (Fase: qué se preserva / qué cambia)

**Se preserva**: la lógica central (Conventional Commits, análisis del diff), el formato de salida del mensaje.

**Se gana** (porque un prompt no lo tenía y una skill lo necesita):
- Frontmatter con `description` orientada a activación explícita.
- Sección "cuándo se activa / cuándo no" (para no disparar en cada interacción de git, solo cuando se pide redactar el mensaje).
- Consideración de si necesita `references/` (en este caso, no — el conocimiento cabe en `SKILL.md`, es una skill pequeña).

## Artefacto final

```text
---
name: conventional-commit-writer
description: Genera mensajes de commit siguiendo el formato Conventional Commits a partir de un diff o resumen de cambios. Actívala cuando el usuario pida ayuda para escribir, redactar o generar un mensaje de commit, o pida revisar si un mensaje de commit sigue el formato correcto — incluso si solo dice "ayúdame con el commit" mientras hay cambios staged.
---

# Conventional Commit Writer

Genera mensajes de commit en formato Conventional Commits (`tipo(alcance): descripción`) a partir del diff o resumen de cambios que el usuario proporcione.

## Cuándo se activa
- El usuario pide ayuda para escribir un mensaje de commit.
- El usuario pide revisar si un mensaje de commit existente sigue el formato correcto.

## Cuándo NO se activa
- El usuario pide hacer el commit en sí (ejecutar `git commit`) sin necesitar ayuda con el mensaje — eso es una acción de git normal, no requiere esta skill.

## Reglas fundamentales
1. Tipo obligatorio: feat, fix, docs, style, refactor, test, chore (u otro tipo estándar si el proyecto define uno distinto en su CLAUDE.md).
2. Alcance opcional entre paréntesis, solo si aporta claridad real.
3. Descripción en modo imperativo, minúscula inicial, sin punto final, máximo ~72 caracteres en la primera línea.
4. Si el cambio tiene impacto de breaking change, usar `!` tras el tipo/alcance y una sección `BREAKING CHANGE:` en el cuerpo.
5. El cuerpo (si hace falta) explica el "por qué", no repite el "qué" que ya es evidente en el diff.

## Formato de respuesta
```text
{{tipo}}({{alcance opcional}}): {{descripción}}

{{cuerpo opcional explicando el por qué}}
```

## Ejemplos cortos de activación
- "ayúdame a escribir el mensaje de commit para estos cambios"
- "genera un commit message para este diff"
- "¿este mensaje de commit sigue conventional commits?"
```

## Cómo usarlo

Instalar en `.claude/skills/conventional-commit-writer/` (nivel proyecto) o `~/.claude/skills/` (nivel usuario). Se activa automáticamente al pedir ayuda con un mensaje de commit.

## Criterios de validación

Verificar que la skill no se activa en peticiones normales de git (por ejemplo, "haz commit de estos cambios" sin pedir ayuda con el mensaje), y que el mensaje generado sigue el formato exacto declarado.
