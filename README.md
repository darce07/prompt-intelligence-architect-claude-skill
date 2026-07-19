<div align="center">

# 🧠 Prompt Intelligence Architect (PIA)

### Un arquitecto senior de prompts, agentes y skills, dentro de un solo Skill de Claude Code

*No escribe el prompt definitivo a la primera. Descubre la necesidad real, diseña la arquitectura, construye el artefacto, lo critica de forma adversarial contra 10 quality gates — y solo entonces lo entrega.*

[![Licencia: MIT](https://img.shields.io/badge/Licencia-MIT-yellow.svg)](LICENSE)
![Versión](https://img.shields.io/badge/versión-1.0.0-blue)
![Plataforma](https://img.shields.io/badge/plataforma-Claude%20Code-8A63D2)
![Estado](https://img.shields.io/badge/estado-activo-success)
![Archivos](https://img.shields.io/badge/archivos-49-orange)

[¿Qué es?](#-qué-es-esto) ·
[¿De qué trata?](#-de-qué-trata) ·
[Instalación](#-instalación) ·
[Cómo se activa](#-cómo-se-activa) ·
[Arquitectura](#-arquitectura) ·
[Modos de trabajo](#-modos-de-trabajo) ·
[Evolución](#-cómo-evoluciona) ·
[Autor](#-autor)

</div>

---

## 📖 ¿Qué es esto?

**`prompt-intelligence-architect`** es un [Skill de Claude Code](https://docs.claude.com/en/docs/claude-code) que convierte a Claude en un **arquitecto senior de prompts, agentes, skills, `CLAUDE.md` y sistemas multiagente**.

En vez de redactar prompts a toda prisa cada vez que alguien pide "hazme un prompt para X", esta skill hace que Claude:

1. **Descubra** la necesidad real detrás de la petición literal, sin sobrepreguntar ni asumir de más.
2. **Clasifique** el tipo de artefacto correcto (prompt simple, agente, skill, multiagente...).
3. **Diseñe** la arquitectura antes de escribir una sola línea del texto final.
4. **Construya** el artefacto usando plantillas probadas, adaptadas al caso concreto.
5. **Critique** su propio resultado desde 6 perspectivas distintas antes de entregarlo.
6. **Documente** solo los aprendizajes confirmados y reutilizables — nunca en silencio.

> **Regla de oro:** ningún artefacto se entrega con una debilidad crítica conocida sin advertirla. Diseñar antes de redactar, siempre.

## 🧭 ¿De qué trata?

La mayoría de los prompts se escriben de una sentada: alguien pide "actúa como experto en X y haz Y", y eso es todo lo que hay. El resultado es previsiblemente frágil — sin alcance definido, sin formato de salida verificable, sin manejo de casos límite, y con reglas que a veces se contradicen entre sí sin que nadie lo note hasta que falla en producción.

`prompt-intelligence-architect` aplica un proceso real de ingeniería a este problema: un flujo de 9 fases (descubrimiento → clasificación → arquitectura → diseño conductual → construcción → crítica adversarial → refactorización → entrega → aprendizaje), 10 criterios de calidad puntuables, 10 quality gates obligatorios antes de entregar, y una base de conocimiento evolutiva que crece con cada proyecto — pero solo con aprendizajes que el usuario aprueba explícitamente, nunca por autoedición silenciosa.

No es una plantilla de "actúa como experto en prompts". Es un sistema completo con clasificación por tipo de artefacto, arquitectura específica para agentes/skills/multiagentes, defensas de seguridad contra prompt injection y filtración de secretos, y una biblioteca de 12 plantillas reutilizables listas para adaptar.

## ✨ Características principales

| Capacidad | Descripción |
|---|---|
| 🔍 **Descubrimiento sin fricción** | Pregunta solo lo crítico, agrupado en una ronda — nunca bloquea el avance con interrogatorios innecesarios. |
| 🏗️ **Arquitectura por tipo de artefacto** | Referencias dedicadas para prompts, agentes, skills de Claude Code, sistemas multiagente y adaptación a otras plataformas (GPTs, Codex, Cursor/Windsurf/Copilot, Gemini). |
| 🧪 **Crítica adversarial de 6 perspectivas** | Arquitecto, usuario final, especialista de dominio, crítico adversarial, mantenedor futuro y evaluador de calidad revisan cada entregable antes de salir. |
| ✅ **10 Quality Gates obligatorios** | Intención, contexto, comportamiento, formato, fallos, herramientas, mantenibilidad, evaluación, seguridad, evolución. |
| 🔐 **Seguridad y privacidad integradas** | Rechaza guardar secretos o credenciales, exige confirmación para herramientas destructivas, y defiende explícitamente contra prompt injection en agentes RAG. |
| 📚 **Base de conocimiento evolutiva y gobernada** | `knowledge/` con patrones, antipatrones, lecciones, guías de plataforma, ADRs y glosario — nada se escribe ahí sin que el usuario lo apruebe primero. |
| 🧩 **12 plantillas + 8 workflows + 15 evaluaciones** | Desde un prompt simple hasta un sistema multiagente completo, cada modo de trabajo (crear, mejorar, auditar, convertir, simplificar, expandir, plantillizar, retrospectiva) tiene su propio proceso documentado. |

## 🚀 Instalación

Esta skill funciona con [Claude Code](https://claude.com/claude-code). Instálala clonándola directamente en tu carpeta de skills:

### Instalación global (recomendada — disponible en todos tus proyectos)

```bash
# Windows
cd C:\Users\<tu-usuario>\.claude\skills
git clone https://github.com/darce07/prompt-intelligence-architect-claude-skill.git prompt-intelligence-architect

# macOS / Linux
cd ~/.claude/skills
git clone https://github.com/darce07/prompt-intelligence-architect-claude-skill.git prompt-intelligence-architect
```

### Instalación por proyecto (solo disponible en ese proyecto)

```bash
cd /ruta/a/tu/proyecto
mkdir -p .claude/skills
cd .claude/skills
git clone https://github.com/darce07/prompt-intelligence-architect-claude-skill.git prompt-intelligence-architect
```

Reinicia Claude Code (o abre una nueva sesión) y la skill `prompt-intelligence-architect` aparecerá automáticamente en el listado de skills disponibles. No requiere dependencias, claves de API ni configuración adicional.

## 🎯 Cómo se activa

No necesitas invocarla manualmente. Claude Code decide activarla solo cuando el pedido calza con su descripción — pero también puedes pedirla en lenguaje natural:

> "usa prompt intelligence architect para diseñar un agente que..."

**Se activa automáticamente ante:** "créame un prompt para...", "necesito un agente que...", "diseña una skill.", "convierte esto en CLAUDE.md.", "audita estas instrucciones.", "quiero un sistema multiagente.", "hazme una plantilla reutilizable.", "crea un evaluador." — incluso si el usuario no usa esas palabras exactas.

**No se activa (y no debería) ante:** tareas normales de programación donde no se está diseñando ninguna instrucción o agente — escribir o depurar código de una aplicación, por ejemplo.

## 🏗️ Arquitectura

```
                        🧠  Prompt Intelligence Architect
                                      │
                    ┌─────────────────┴─────────────────┐
                    │     Clasificación de intención     │
                    │  (qué modo, qué tipo de artefacto) │
                    └─────────────────┬─────────────────┘
                                      │
        ┌───────────┬────────────┬───┴────┬────────────┬────────────┐
        │           │            │        │            │            │
     Crear      Mejorar      Auditar   Convertir   Simplificar   Expandir
        │           │            │        │            │            │
        └───────────┴─────┬──────┴────────┴─────┬──────┴────────────┘
                           │                     │
                 📐  Arquitectura por tipo   🔐  Seguridad y privacidad
              (prompt / agente / skill /      (secretos, mínimo privilegio,
                multiagente / plataforma)      prompt injection)
                           │                     │
                           └──────────┬──────────┘
                                      │
                         🧪  Crítica adversarial
                    6 perspectivas · 10 quality gates
                                      │
                              📋  Artefacto entregado
                        (con supuestos declarados y
                         criterios de validación)
                                      │
                         📚  Aprendizaje gobernado
                    (propuesta → aprobación → knowledge/)
```

### Estructura del repositorio

```
prompt-intelligence-architect/
├── SKILL.md                       # Punto de entrada operativo, compacto
├── README.md                      # Este archivo
├── CHANGELOG.md                   # Historial de versiones (semver)
├── LICENSE                        # MIT
├── references/                    # Arquitectura profunda por tipo de artefacto (8)
│   ├── prompt-architecture.md     # Las 9 fases + anatomía de prompt/system prompt
│   ├── agent-architecture.md
│   ├── skill-architecture.md
│   ├── multi-agent-architecture.md
│   ├── platform-adaptation.md     # Claude Code, GPTs, Codex, Cursor/Windsurf/Copilot, Gemini
│   ├── security-and-privacy.md
│   ├── evaluation-framework.md    # 6 perspectivas, 10 criterios, 10 quality gates
│   └── continuous-improvement.md  # Aprendizaje gobernado y versionado semántico
├── workflows/                     # Proceso paso a paso por modo de trabajo (8)
│   ├── create.md
│   ├── improve.md
│   ├── audit.md
│   ├── convert.md
│   ├── simplify.md
│   ├── expand.md
│   ├── template.md
│   └── retrospective.md
├── templates/                     # Plantillas reutilizables listas para adaptar (12)
├── evaluations/                   # 15+ casos de prueba de comportamiento (6 archivos)
├── examples/                      # 5 ejemplos completos de principio a fin
└── knowledge/                     # Base de conocimiento evolutiva y gobernada
    ├── patterns/
    ├── anti-patterns/
    ├── lessons/
    ├── platform-guides/
    ├── decision-records/
    └── glossary/
```

## 🧩 Modos de trabajo

| Modo | Cuándo usarlo | Workflow |
|---|---|---|
| **Crear** | Diseñar un artefacto nuevo desde cero | [`workflows/create.md`](workflows/create.md) |
| **Mejorar** | Refactorizar un prompt/agente/skill existente sin cambiar su intención | [`workflows/improve.md`](workflows/improve.md) |
| **Auditar** | Evaluar calidad, seguridad y consistencia antes de publicar | [`workflows/audit.md`](workflows/audit.md) |
| **Convertir** | Transformar entre formatos (prompt → skill, agente → multiagente...) | [`workflows/convert.md`](workflows/convert.md) |
| **Simplificar** | Reducir longitud/complejidad preservando comportamiento | [`workflows/simplify.md`](workflows/simplify.md) |
| **Expandir** | Añadir capacidades sin romper lo existente | [`workflows/expand.md`](workflows/expand.md) |
| **Plantillizar** | Convertir una solución puntual en plantilla reutilizable | [`workflows/template.md`](workflows/template.md) |
| **Retrospectiva** | Cerrar un proyecto y proponer aprendizajes a `knowledge/` | [`workflows/retrospective.md`](workflows/retrospective.md) |

## 🔄 Cómo evoluciona

`knowledge/` es la **única memoria persistente real** de esta skill — no hay aprendizaje automático oculto en ningún otro lugar. Cuando surge un aprendizaje confirmado y reutilizable, PIA lo propone al usuario con el texto exacto que añadiría, y **solo lo escribe tras aprobación explícita** (ver [`references/continuous-improvement.md`](references/continuous-improvement.md)). Cada cambio de comportamiento relevante se documenta en [`CHANGELOG.md`](CHANGELOG.md) con versionado semántico.

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Si encuentras un caso donde la clasificación de intención falla, un tipo de artefacto que falta cubrir, o un quality gate que nunca detecta nada, abre un *issue* o un *pull request*. Toda mejora a `knowledge/` debe seguir el protocolo de propuesta-aprobación documentado en [`references/continuous-improvement.md`](references/continuous-improvement.md) — nunca se aplica en silencio.

## 👤 Autor

**darce07**

- GitHub: [@darce07](https://github.com/darce07)

## 📄 Licencia

Este proyecto está bajo la Licencia MIT — consulta [LICENSE](LICENSE) para más detalles. Eres libre de usar, copiar, modificar y distribuir esta skill, incluso con fines comerciales, dando el crédito correspondiente.

---

<div align="center">

*Diseña antes de redactar. Critica antes de entregar. Aprende solo lo que se confirma.*

</div>
