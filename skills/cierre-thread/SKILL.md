---
name: cierre-thread
description: Cierra el thread de trabajo en curso: verifica el estado real (worktree, commits, gates, PR/CI), registra el cierre de la historia en el backlog y entrega el handoff para el siguiente thread. El humano decide cuándo invocarla.
disable-model-invocation: true
---

# Cierre de thread

Cierre ordenado de la sesión: nada queda sin registrar, sin verificar o sin dueño.

## 1. Verificar

Antes de dar por acabado, corrobora el estado real y muéstramelo:

1. **Worktree**: `git status` — árbol limpio. Si hay cambios sin commitear, surfacéelos y pregúntame qué hacer (commitear, descartar o dejarlos declarados). Nunca los descartes tú.
2. **Commits**: lista los commits de la sesión (`git log <base>..HEAD --oneline`). Confirma que el último estado del código pasó los quality gates completos definidos en el `AGENTS.md` del proyecto; si no, córrelos ahora y muestra el resultado.
3. **PR abierto (si hay)**: checks de CI, comentarios sin responder, conflictos con la branch base. Estado tal cual, sin adornarlo.
4. **Artefactos de sesión**: servidores de fondo levantados para probar, worktrees de verificación, temporales generados — detén y limpia los tuyos.

Si algo falla, arréglalo o déjalo explícito en el handoff; no lo escondas.

## 2. Registrar

- **Backlog del requerimiento**: actualiza `Estado` y `Ref` de la historia trabajada (o del punto en que quedó si no hay historia cerrada).
- Agrega el bloque **"Cierre #N"** con el formato de `MODUS_OPERANDI.md` §6: fecha, sesiones con lo hecho y duración, tiempo total y commits, resumen en 2–4 líneas, lecciones (contratos pisados, trampas del entorno, decisiones que costaron tiempo).
- El **tiempo es estimación**: derívalo de los timestamps del primer → último commit de la historia más la duración percibida de cada sesión, y **preséntame la cifra para confirmarla o corregirla** antes de escribirla.
- Commit y push del cambio al backlog (mensaje `docs(...): registro de cierre H#N`).

## 3. Handoff

Redacta el bloque de arranque para el siguiente thread, listo para pegar:

- **Qué quedó**: historias cerradas/en vuelo con refs (PR #N, estado de CI, merge pendiente).
- **Qué sigue**: la historia natural siguiente del backlog con sus dependencias (o la tarea puntual que yo indique).
- **Pendientes míos**: revisiones, decisiones, merges que me tocan a mí.
- **Riesgos vigentes**: lecciones del cierre que apliquen a lo que viene (p. ej. docs compartidos entre PRs en vuelo).

## 4. Monitoreo y entrega

- Si hay PR en vigilancia por este thread, pregúntame: lo dejo vigilado (este thread sigue vivo para el CI) o lo entrego a mi bandeja (unwatch).
- Cierra mostrando: resumen de cierre + prompt de arranque sugerido para el nuevo thread.