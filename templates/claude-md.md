# Plantilla: `CLAUDE.md`

Para instrucciones que deben aplicar siempre en un repositorio concreto — no para comportamiento ocasional (eso es una skill, ver `templates/skill.md`).

## Cuándo usar esta plantilla

Cuando el repositorio tiene convenciones, comandos o restricciones que Claude Code debe conocer en cada sesión de trabajo sobre ese proyecto.

## Plantilla

```text
# CLAUDE.md

## Resumen del proyecto
{{Qué es el proyecto, en 2-3 líneas. Stack principal.}}

## Comandos esenciales
```bash
{{comando de instalación}}
{{comando de desarrollo/arranque}}
{{comando de pruebas}}
{{comando de build}}
```

## Convenciones de código
- {{convención 1, con la razón si no es obvia}}
- {{convención 2}}

## Arquitectura / estructura de carpetas
{{Mapa breve de dónde vive qué, si el repositorio no es autoexplicativo.}}

## Reglas del proyecto
- {{regla obligatoria 1}}
- {{regla obligatoria 2}}

## Qué NO hacer
- {{acción prohibida, con la razón}}

## Flujo de trabajo esperado
{{Si hay un proceso concreto que seguir antes de considerar una tarea terminada
— por ejemplo, correr pruebas, actualizar un changelog, etc.}}
```

## Notas de uso

- `CLAUDE.md` se carga siempre para el repositorio — mantenlo compacto (equivalente al límite de `SKILL.md`: si crece demasiado, extrae detalle a documentos que `CLAUDE.md` referencia explícitamente, no que carga automáticamente).
- No dupliques aquí lógica que solo aplica ocasionalmente — eso pertenece a una skill activada bajo demanda.
- Si el repositorio tiene reglas de alcance distinto por subcarpeta (por ejemplo, backend vs. frontend), considera `CLAUDE.md` adicionales en esas subcarpetas en vez de una sola raíz con condicionales.
