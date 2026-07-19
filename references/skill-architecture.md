# Arquitectura de skills de Claude Code

Cómo diseñar una skill de Claude Code: qué es, cuándo conviene frente a un prompt o `CLAUDE.md`, y cómo estructurarla para que cargue de forma eficiente y se active correctamente.

## Tabla de contenido

1. Qué es una skill y cuándo usarla
2. Progressive disclosure (los tres niveles)
3. Anatomía de `SKILL.md`
4. Estructura de carpetas
5. Diseño de la descripción (activación)
6. Errores comunes al diseñar skills

---

## 1. Qué es una skill y cuándo usarla

Una skill de Claude Code es un paquete de instrucciones que Claude carga bajo demanda cuando la tarea del usuario coincide con su propósito. A diferencia de `CLAUDE.md` (que se carga siempre, en todo el repositorio) o un prompt puntual (que vive en un solo mensaje), una skill:

- Se activa solo cuando es relevante, no en cada turno.
- Puede incluir archivos de referencia, plantillas y ejemplos que no ocupan contexto hasta que se necesitan.
- Es reutilizable entre proyectos si se instala a nivel usuario, o específica de un repositorio si se instala en `.claude/skills/`.

**Usa una skill cuando:** el comportamiento es reutilizable entre tareas o proyectos, el conocimiento necesario es demasiado extenso para vivir en un prompt único, o el flujo de trabajo tiene pasos claros que conviene documentar una sola vez.

**No uses una skill cuando:** la instrucción aplica siempre en el repositorio (eso es `CLAUDE.md`), o la tarea es de un solo uso sin intención de reutilizarla (eso es un prompt simple).

## 2. Progressive disclosure (los tres niveles)

Una skill bien diseñada carga información en capas, no de golpe:

1. **Metadata** (`name` + `description` del frontmatter): siempre en contexto una vez que Claude Code lista las skills disponibles. Debe ser compacta (del orden de 100 palabras) pero suficientemente específica para activar correctamente.
2. **Cuerpo de `SKILL.md`**: se carga completo cuando la skill se activa. Debe mantenerse operativo y compacto — idealmente bajo 500 líneas. Si se acerca a ese límite, añade una capa de jerarquía (referencias) en vez de seguir creciendo.
3. **Recursos empaquetados** (`references/`, `templates/`, `workflows/`, etc.): se cargan solo cuando `SKILL.md` indica explícitamente que hay que leerlos para la tarea en curso. No tienen límite de tamaño total porque no se cargan todos a la vez.

El error más común es escribir todo el conocimiento dentro de `SKILL.md` "por si acaso". Eso rompe la progressive disclosure y hace que cada activación cargue contexto innecesario.

## 3. Anatomía de `SKILL.md`

`SKILL.md` debe contener, y nada más que:

- **Frontmatter**: `name` y `description` (obligatorios). La descripción es el mecanismo principal de activación (ver sección 5).
- **Identidad/propósito**: qué hace la skill, en pocas líneas.
- **Cuándo se activa / cuándo no**: para reducir falsos positivos y falsos negativos de activación.
- **Flujo de decisión**: cómo pasar de la petición del usuario a la referencia o plantilla correcta. Normalmente una tabla "si la tarea es X, lee Y".
- **Reglas fundamentales**: las 5-10 reglas que gobiernan cualquier uso de la skill, no un tratado completo.
- **Formato de respuesta**: cómo debe estructurarse la salida.
- **Protocolo de aprendizaje** (si la skill tiene base de conocimiento evolutiva): cómo se propone y aprueba un cambio.
- **Límites de seguridad**: qué la skill nunca debe hacer.
- **Ejemplos cortos de activación**: 3-5 frases de ejemplo que deberían disparar la skill.

`SKILL.md` **no debe duplicar** el contenido de `references/` — debe apuntar a él.

## 4. Estructura de carpetas

```text
skill-name/
├── SKILL.md              # obligatorio
├── README.md              # opcional, orientado a humanos que instalan/mantienen la skill
├── CHANGELOG.md           # opcional, si la skill versiona su comportamiento
├── references/            # documentación profunda cargada bajo demanda
├── workflows/              # procesos paso a paso (si la skill tiene múltiples modos)
├── templates/              # plantillas o esqueletos reutilizables
├── examples/                # casos completos de entrada/salida
├── evaluations/             # casos de prueba de comportamiento
├── scripts/                 # código ejecutable determinista (si aplica)
└── knowledge/                # base de conocimiento evolutiva (si la skill aprende)
```

No todas las skills necesitan todas las carpetas. Una skill pequeña puede ser solo `SKILL.md`. Añade estructura en proporción a la complejidad real (principio de Fase 3 en `references/prompt-architecture.md`).

Cuando una skill soporta múltiples dominios o variantes independientes (por ejemplo, distintos proveedores de nube), organiza `references/` por variante (`aws.md`, `gcp.md`, `azure.md`) para que Claude lea solo la relevante.

## 5. Diseño de la descripción (activación)

La `description` del frontmatter es el mecanismo principal por el que Claude decide activar la skill. Reglas prácticas:

- Incluye **qué hace** la skill y **en qué contextos** se debe usar, con frases concretas que un usuario real escribiría.
- Sé deliberadamente un poco "insistente": los modelos tienden a subactivar skills. Si la skill aplica a una familia amplia de peticiones, dilo explícitamente ("incluso si no menciona la palabra X").
- Declara también cuándo **no** se activa, si existe riesgo de falsos positivos con tareas cercanas.
- No optimices por elegancia literaria — optimiza por qué frases de usuario deberían coincidir.

## 6. Errores comunes al diseñar skills

| Error | Consecuencia | Corrección |
|---|---|---|
| `SKILL.md` de más de 500 líneas sin referencias | Carga contexto innecesario en cada activación | Extrae a `references/` y deja tabla de punteros |
| Descripción vaga ("ayuda con prompts") | Subactivación o activación en tareas no relacionadas | Descripción específica con ejemplos de disparo y no-disparo |
| Carpetas vacías o con placeholders | La skill parece completa pero no lo está; Claude puede citar un archivo sin contenido real | Cada archivo referenciado debe tener contenido completo |
| Prometer aprendizaje automático sin `knowledge/` real | Expectativa falsa de memoria persistente | Sé explícito: sin archivos de persistencia, no hay memoria entre sesiones |
| Duplicar contenido entre `SKILL.md` y `references/` | Doble mantenimiento, riesgo de que diverjan | Una sola fuente de verdad por tema; `SKILL.md` apunta, no repite |
