# Plantilla: Sistema multiagente

Ver `references/multi-agent-architecture.md` antes de usar esta plantilla — confirma primero que el caso realmente justifica más de un agente.

## Cuándo usar esta plantilla

Cuando hay dominios de conocimiento genuinamente distintos, paralelismo real entre partes de la tarea, o necesidad de un rol de auditoría independiente del rol que produce el trabajo.

## Plantilla

```text
# Orquestador
Identidad: {{quién recibe la petición original}}
Responsabilidad: {{decidir qué roles intervienen, en qué orden, y consolidar el resultado}}

# Roles
## {{Rol 1}}
Identidad / misión / alcance: {{...}} (ver templates/agent.md para el detalle completo de cada rol)

## {{Rol 2}}
Identidad / misión / alcance: {{...}}

## {{Rol N — opcional: Auditor/Crítico}}
Identidad / misión / alcance: {{revisa el trabajo de los demás roles antes de la consolidación}}

# Routing
{{Lógica explícita: qué rol(es) intervienen para qué tipo de petición.
No "el orquestador decide con buen juicio" — la regla concreta.}}

# Contratos entre agentes
| De | A | Formato de entrada esperado | Formato de salida entregado | Qué pasa si no se puede cumplir |
|---|---|---|---|---|
| {{rol}} | {{rol}} | {{...}} | {{...}} | {{estado explícito, no inventar contenido}} |

# Flujo
{{Paralelo / secuencial / con dependencias parciales — diagrama textual del orden.}}

# Resolución de conflictos
{{Jerarquía de autoridad / escalamiento a humano / síntesis explícita — elige una
regla concreta y por qué se eligió para este caso.}}

# Consolidación
{{Cómo se combina el trabajo de los roles en una única respuesta coherente
para el usuario.}}

# Auditoría
{{Si existe un rol de revisión independiente, en qué punto del flujo actúa
y qué autoridad tiene sobre el resultado final.}}
```

## Ejemplo relleno (fragmento — sistema de revisión de PRs)

```text
# Orquestador
Recibe el diff de un pull request y decide qué especialistas deben revisarlo según los archivos tocados.

# Routing
- Si el diff toca archivos de autenticación o manejo de secretos → invoca Rol Seguridad.
- Si el diff toca componentes de UI → invoca Rol Frontend.
- Si el diff toca migraciones o esquemas → invoca Rol Datos.
- Un mismo diff puede invocar varios roles en paralelo si toca varias áreas.

# Resolución de conflictos
El Rol Seguridad tiene veto: si señala un hallazgo crítico, el veredicto consolidado es "no aprobar" independientemente de lo que digan los demás roles.
```

## Notas de uso

Antes de entregar, aplica la sección 5 de `references/multi-agent-architecture.md` (auditoría del sistema completo) — verifica solapamiento de roles, fallback cuando ningún rol especializado aplica, y manejo de fallo de un agente individual.
