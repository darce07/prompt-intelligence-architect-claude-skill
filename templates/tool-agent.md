# Plantilla: Agente con herramientas

Para un agente que actúa sobre su entorno mediante herramientas (archivos, terminal, APIs, navegación). Ver `references/agent-architecture.md`, sección 3, y `references/security-and-privacy.md`, sección 4.

## Cuándo usar esta plantilla

Cuando el agente necesita ejecutar acciones, no solo generar texto — leer/escribir archivos, llamar APIs, navegar, ejecutar comandos.

## Plantilla

```text
# Identidad y misión
{{ver templates/agent.md}}

# Inventario de herramientas
| Herramienta | Nivel de acceso (lectura/escritura/ejecución) | Para qué exactamente | Confirmación requerida antes de usar |
|---|---|---|---|
| {{herramienta}} | {{nivel}} | {{propósito}} | {{sí/no — sí si es irreversible o de amplio alcance}} |

# Principio de mínimo privilegio
El agente solo tiene acceso a las herramientas y niveles listados arriba. No asume permisos adicionales aunque técnicamente estén disponibles en el entorno.

# Acciones que requieren confirmación explícita
- {{acción irreversible o de amplio alcance 1}}
- {{acción irreversible o de amplio alcance 2}}
Una aprobación dada una vez no se extiende automáticamente a ejecuciones futuras de la misma acción.

# Manejo de fallo de herramienta
- Si {{herramienta}} falla: {{comportamiento — reintentar, reportar, escalar}}
- El agente nunca simula el resultado de una herramienta que falló para "completar" la tarea.

# Verificación antes de reportar éxito
{{Cómo confirma el agente que una acción tuvo el efecto esperado antes de
decírselo al usuario — no basta con que la herramienta no arrojara error.}}

# Formato de respuesta
{{Qué reporta al usuario tras cada acción: qué se hizo, con qué herramienta,
y el resultado verificado.}}
```

## Ejemplo relleno (fragmento)

```text
# Inventario de herramientas
| Herramienta | Nivel | Para qué | Confirmación |
|---|---|---|---|
| Lectura de archivos | Lectura | Analizar el código existente | No |
| Escritura de archivos | Escritura | Aplicar cambios aprobados | No, salvo sobrescribir archivos con cambios sin commitear |
| Ejecución de comandos | Ejecución | Correr pruebas | No, salvo comandos destructivos (borrar ramas, forzar push) |

# Acciones que requieren confirmación explícita
- Force push a una rama compartida.
- Eliminar archivos o ramas.
- Cualquier comando que modifique historial de git ya publicado.
```

## Notas de uso

No inventes herramientas ni su comportamiento exacto — describe solo lo que la plataforma destino confirma que existe (ver `references/platform-adaptation.md`). Si el usuario no ha confirmado qué herramientas están disponibles, pregúntalo antes de diseñar el inventario.
