---
name: inicio-thread
description: Inicia un thread de trabajo: carga el contexto del requerimiento (spec, backlog, cierres), coteja con la realidad (PRs, CI, worktrees) y presenta el punto de partida y el objetivo. No empieza a trabajar hasta que el humano lo indique.
disable-model-invocation: true
---

# Inicio de thread

Arranque con contexto completo: nada se re-explica, nada se re-pisa.

## 1. Cargar contexto

Lee, en este orden:

1. **Backlog del requerimiento activo** — yo lo nombro; si no, búscalo (el `docs/*BACKLOG*.md` más reciente del proyecto). Tabla de estados + fichas /story + bloques de cierre: ahí vive qué se hizo, cómo, y qué se aprendió.
2. **Spec del requerimiento** (`docs/REQ_*.md` asociado al backlog): decisiones levantadas, fuera de alcance, criterios.
3. **`AGENTS.md` del proyecto**: quality gates con sus comandos exactos, git workflow, reglas duras.
4. **`MODUS_OPERANDI.md`** (si el proyecto lo declara): el flujo `/backlog` → `/story` → `/pair` y la convención de cierres §6.

## 2. Cotejar con la realidad

La documentación puede estar detrás del mundo real. Verifica:

- PRs abiertos del requerimiento: lista y checks de CI, comentarios, conflictos con la base.
- Branches y worktrees activos relacionados (`git worktree list`).
- Si el backlog y git discrepan, surfacéalo: el tracker se corrige antes de avanzar, no después.

## 3. Brief de arranque

Preséntame:

- **Dónde quedó**: última historia cerrada/en vuelo, con refs (PR #N, CI, merge pendiente).
- **Qué toca**: la historia natural siguiente del backlog (o la que yo indique), con sus dependencias.
- **Lecciones vigentes**: las de los cierres que apliquen a lo que viene.
- **Riesgos conocidos**: conflictos previstos (p. ej. el backlog editado por dos PRs en vuelo), decisiones pendientes mías.

## 4. Esperar instrucción

**No empieces a trabajar hasta que yo lo indique.** Si apruebo arrancar:

- Propón worktree + branch según la convención del `AGENTS.md`; si la historia no depende de otra en vuelo, corta desde la base limpia. Si los docs del requerimiento no están en la base, cópialos como primer commit `docs(...)`, igual que la historia anterior.
- Entra en `/story` con la historia elegida (o `/pair` directo si ya tiene ficha aprobada).