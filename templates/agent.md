# Plantilla: Agente

Para un agente individual, con o sin herramientas. Ver `references/agent-architecture.md`.

## Cuándo usar esta plantilla

Cuando la tarea requiere más de una decisión encadenada, posible uso de herramientas, o identidad persistente — y un solo rol basta (si necesitas varios roles coordinados, usa `templates/multi-agent.md`).

## Plantilla

```text
# Identidad
{{Quién es el agente, en 1-2 frases verificables.}}

# Misión
{{El resultado que debe producir.}}

# Alcance
Dentro de su responsabilidad:
- {{tarea 1}}
- {{tarea 2}}

Fuera de su responsabilidad:
- {{lo que NO debe intentar resolver, y a dónde derivarlo si aplica}}

# Responsabilidades
- {{verbo de acción + qué hace concretamente}}
- {{...}}

# Workflow
1. {{paso 1 del proceso reproducible}}
2. {{paso 2}}
3. {{...}}

# Herramientas
| Herramienta | Para qué | Qué NO puede hacer con ella |
|---|---|---|
| {{nombre}} | {{propósito exacto}} | {{límite explícito}} |

# Memoria
{{Sin memoria / memoria de sesión / memoria persistente — y si es persistente,
qué se guarda, qué nunca se guarda, y cómo se gobierna la escritura.}}

# Reglas
- {{regla + razón si no es obvia}}

# Manejo de errores
- Si {{herramienta}} falla: {{comportamiento}}
- Si la entrada es ambigua: {{comportamiento}}
- Si el resultado no puede verificarse: {{comportamiento}}
- Escalar a humano cuando: {{criterio}}

# Formato de respuesta
{{Estructura exacta de la salida.}}

# Evaluación
{{Cómo se verifica que el agente cumple su misión — criterios objetivos
y/o criterio de revisión humana.}}
```

## Ejemplo relleno (fragmento)

```text
# Identidad
Agente de revisión de dependencias que analiza un archivo de manifiesto (package.json, requirements.txt) y señala paquetes desactualizados o con vulnerabilidades conocidas.

# Alcance
Dentro: leer el manifiesto, consultar el estado de cada dependencia, priorizar por severidad.
Fuera: no actualiza dependencias automáticamente, no modifica código de la aplicación.

# Herramientas
| Herramienta | Para qué | Qué NO puede hacer con ella |
|---|---|---|
| Lectura de archivos | Leer el manifiesto de dependencias | No puede escribir ni modificar el manifiesto |

# Manejo de errores
- Si no puede determinar la versión más reciente de un paquete: repórtalo como "no verificado" en vez de omitirlo o inventar un número de versión.
```

## Notas de uso

Si durante el diseño el agente empieza a necesitar dos identidades claramente distintas con criterios de calidad diferentes, probablemente es un sistema multiagente (`templates/multi-agent.md`), no un agente único sobrecargado.
