# hola-ai (fork JotaConts)

Skills de agentes para construir software con IA **sin soltar el timón**. Inspirado en Extreme Programming: historias de usuario verticales, criterios de aceptación, test-first, pair programming, diseño simple.

La IA divide, propone y escribe código en pasos pequeños. Tú decides.

> Fork de [nschurmann/hola-ai](https://github.com/nschurmann/hola-ai) (MIT).

## Adaptaciones de este fork

1. **Skills en español.** Traducción completa; los IDs de comando se mantienen idénticos al upstream (`/backlog`, `/story`, `/pair`) para compatibilidad.
2. **Fase Quality gates en `/pair`.** Antes de sugerir commit, se corren los quality gates definidos en el `AGENTS.md` del proyecto (linters, typecheck, tests completos, estilo). Gates en verde = condición para proponer commit. Nunca se editan aprobaciones, snapshots o configs de estilo para hacerlos pasar.
3. **`AGENTS.md` como contexto primero.** Las referencias a `CLAUDE.md` pasaron a `AGENTS.md` (con `CLAUDE.md` como alternativa), coherente con los repos del proyecto.

## El flujo

```
/backlog  →  /story  →  /pair
  qué        qué exacto   cómo
```

| Skill | Qué hace | Qué nunca hace |
| --- | --- | --- |
| [`/backlog`](skills/backlog/SKILL.md) | Convierte una idea en un backlog corto de historias de usuario verticales de una línea. | Inventar requisitos, historias técnicas, estimaciones. |
| [`/story`](skills/story/SKILL.md) | Toma **una** historia, agrega 2–3 criterios de aceptación Dado/Cuando/Entonces y un mini plan (≤5 bullets) para tu aprobación. | Escribir código. Si necesita más de 3 criterios, propone dividir la historia. |
| [`/pair`](skills/pair/SKILL.md) | Pair programming: la IA conduce, tú navegas. Un test → rojo → código mínimo → verde, y se detiene a esperar. Antes del commit, quality gates del proyecto. | Commitear, editar tests para hacerlos pasar, agregar lo que no pediste. |

La salida de cada skill es el input de la siguiente, en bloques listos para pegar en tu tracker.

## Principios

- **No inventar.** La información faltante se pregunta, no se rellena.
- **Lo más simple que funcione.** Sin abstracciones "para el futuro".
- **Slices verticales y pequeñas.** Las historias atraviesan todas las capas; los pasos son un test y ~50 líneas.
- **Sugerir, no decidir.** Patrones, refactors y commits los decides tú.
- **Checkpoints explícitos.** Cada fase termina esperando tu aprobación.

## Install

```bash
git clone https://github.com/JotaConts/hola-ai.git

# Global — todos los proyectos
mkdir -p ~/.claude/skills ~/.config/opencode/skills
cp -r hola-ai/skills/* ~/.claude/skills/
cp -r hola-ai/skills/* ~/.config/opencode/skills/

# O un solo proyecto
cp -r hola-ai/skills/* <tu-proyecto>/.claude/skills/
```

Las skills solo se invocan manualmente (`/backlog`, `/story`, `/pair`), nunca automáticamente.

## Modus operandi

El método completo — flujo, roles, checkpoints, Definition of Done y cómo adoptarlo en un proyecto nuevo — está documentado en [MODUS_OPERANDI.md](MODUS_OPERANDI.md).

---

Basado en hola-ai de Hola Mundo. Fork mantenido por JotaConts.