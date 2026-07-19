# Adaptación por plataforma

Cómo ajustar un artefacto de instrucciones a la plataforma de destino. Regla general: cuando una característica de plataforma no está confirmada, PIA lo declara explícitamente en vez de inventarla.

## Tabla de contenido

1. Claude Code
2. OpenAI / GPTs personalizados
3. Codex
4. Cursor / Windsurf / GitHub Copilot
5. Gemini
6. Qué hacer cuando la plataforma no está confirmada

---

## 1. Claude Code

Al diseñar para Claude Code, considera:

- **`SKILL.md`**: para comportamiento reutilizable y activado bajo demanda (ver `references/skill-architecture.md`).
- **`CLAUDE.md`**: para instrucciones que deben aplicar siempre en un repositorio concreto — convenciones de código, comandos del proyecto, arquitectura. No es el lugar para lógica que solo aplica ocasionalmente (eso es una skill).
- **Reglas por repositorio**: `CLAUDE.md` puede vivir en la raíz o en subcarpetas para reglas de alcance más específico.
- **Herramientas disponibles**: no asumas qué herramientas tiene Claude Code en la sesión del usuario (pueden variar: Bash, Read, Edit, MCP servers específicos). Describe el comportamiento esperado sin dar por hecho una herramienta concreta salvo que el usuario la haya confirmado.
- **Uso de subagentes o skills**: si el diseño se beneficia de delegar en un subagente o en otra skill, dilo explícitamente en vez de asumir que el modelo lo hará por iniciativa propia.
- **Contexto local del proyecto**: un artefacto para Claude Code puede asumir acceso al sistema de archivos del repositorio; uno para un GPT o Gemini Gem generalmente no.
- **Lectura selectiva de referencias**: diseña para progressive disclosure (ver `references/skill-architecture.md`) — evita cargar conocimiento innecesario de golpe.

## 2. OpenAI / GPTs personalizados

Separa claramente cuatro capas, porque la plataforma las trata como distintas:

- **Instrucciones** (system prompt del GPT): identidad, reglas de comportamiento.
- **Conocimiento** (archivos subidos): información de referencia, no instrucciones de comportamiento.
- **Herramientas/Actions**: capacidades externas declaradas explícitamente con su esquema.
- **Conversation starters**: ejemplos de entrada que orientan al usuario, no parte del comportamiento en sí.

No mezcles conocimiento de referencia dentro del bloque de instrucciones — la plataforma los trata de forma distinta y mezclarlos dificulta el mantenimiento.

## 3. Codex

Orienta las instrucciones a un flujo de repositorio: qué comandos ejecutar para instalar dependencias, correr pruebas y verificar cambios; qué convenciones de commit o PR seguir; cómo se verifica que un cambio es correcto (tests, linters) antes de darlo por terminado. Las instrucciones para Codex deben ser accionables y verificables por ejecución real, no solo descriptivas.

## 4. Cursor / Windsurf / GitHub Copilot

Estas plataformas leen archivos de reglas breves y accionables integrados en el contexto del editor. Prioriza:

- Reglas cortas, una idea por regla, sin necesidad de las 9 fases completas de `references/prompt-architecture.md`.
- Evita reglas que dependan de contexto que el editor no tiene garantizado (por ejemplo, todo el historial de conversación).
- No asumas soporte para estructuras avanzadas (subagentes, memoria persistente) salvo que el usuario confirme que la versión de la herramienta lo soporta.

## 5. Gemini

Adapta identidad, formato y uso de herramientas sin asumir sintaxis específica de function calling, memoria o extensiones que no estén confirmadas por el usuario o la documentación que aporte. Cuando el usuario no especifique la sintaxis exacta de su integración con Gemini, entrega el diseño en términos de comportamiento (qué debe hacer, qué debe evitar) y señala explícitamente qué partes requerirán adaptarse a la sintaxis real de la API o de Gemini Gems.

## 6. Qué hacer cuando la plataforma no está confirmada

Si el usuario no indica la plataforma destino:

- Si el contexto de la conversación lo deja claro (por ejemplo, se está trabajando dentro de Claude Code), infiere razonablemente y decláralo como supuesto.
- Si no hay pista suficiente y la plataforma cambia materialmente el diseño (por ejemplo, si depende de memoria persistente o de un formato de herramientas específico), pregunta — es uno de los casos de "pregunta cuando falte información crítica" de `references/prompt-architecture.md`.
- Nunca inventes una sintaxis de plataforma concreta (nombres de campos, formatos de function calling, límites de tokens) que no hayas confirmado. Declara la limitación: "esta sección requiere adaptarse a la sintaxis exacta de tu integración con X".
