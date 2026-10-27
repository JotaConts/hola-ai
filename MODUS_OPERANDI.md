# Modus Operandi — desarrollo con IA bajo premisas XP

Este documento es el método de trabajo por defecto para proyectos que adopten las skills de este fork. Las skills (`/backlog`, `/story`, `/pair`) llevan las instrucciones operativas; este doc explica el flujo completo, los roles y cómo adoptarlo en un proyecto nuevo.

## 1. El flujo

```
Requerimiento (spec, idea, reunión)
        │
        ▼
    /backlog ──────► historias verticales (una línea c/u) ──► tracker (Issues o backlog.md local)
        │
        ▼ (por cada historia, en orden)
    /story ────────► 2–3 criterios + mini plan + fuera de alcance ──► ficha de la historia
        │
        ▼
    /pair ─────────► lista de tests ──► ciclos TDD ──► quality gates ──► commit ──► PR
        │
        ▼
    Cierre: revisión con contexto limpio + verificación manual + merge
```

**Una historia = un worktree/branch = un PR.** Una sesión de `/pair` trabaja una sola historia. El tracker puede ser GitHub Issues o un backlog local (ver §6.3).

## 2. Roles

| Momento | IA | Humano |
|---|---|---|
| `/backlog` | Ordena y trocea en historias verticales | Trae los requisitos, ajusta el backlog |
| `/story` | Propone criterios y plan | Aprueba, corrige, decide el alcance |
| `/pair` | Conduce: escribe test y código mínimo | Navega: revisa cada paso, dice sí/no |
| Commit y PR | Sugiere mensajes, nunca commitea | Commitea y publica |
| Diseño | Sugiere con señales concretas del código | Decide |

Regla de oro: **la IA propone, el humano decide.** La información faltante se pregunta, nunca se inventa.

## 3. Checkpoints explícitos

Ninguna fase avanza sin aprobación:

1. Backlog completo (el humano ajusta antes de subirlo al tracker).
2. Criterios + plan de la historia.
3. Lista de tests (es la especificación del /pair).
4. Cada ciclo TDD (por defecto 1 paso por parada; el humano puede pedir lotes de N).
5. Quality gates en verde → sugerencia de commit.
6. PR y cierre.

## 4. Definition of Done (quality gates)

Antes de proponer un commit, `/pair` corre los gates declarados en el `AGENTS.md` del proyecto y los muestra en verde. Si el proyecto no los declara, el mínimo es: linter + typecheck (si aplica) + suite de tests completa.

Reglas duras:

- Gates en verde son **condición** para sugerir commit, no un paso opcional.
- Nunca editar aprobaciones, snapshots o configuraciones de estilo para hacer pasar los gates (p. ej. `typing_approvals.toml`, snapshots E2E).
- Funcionalidad y refactor van en commits separados; el refactor solo se hace con tests verdes.

## 5. Relación con specs y levantamientos grandes

Un documento de requerimiento tipo `REQ_*.md` (decisiones, criterios Gherkin, mapa técnico) **no genera tareas directamente**: es el input de `/backlog`. El backlog lo trocea en historias verticales; los criterios Gherkin del spec son materia prima para los criterios de `/story` (2–3 por historia). El spec queda como documento de referencia para el Product Owner; el tracker refleja el avance real.

Si una historia "cabeza" necesita más de 3 criterios, se divide (regla de `/story`) y las nuevas historias vuelven al backlog.

## 6. Registro de cierre de historia

Al cerrar una historia (PR abierto o merge), se agrega un bloque **"Cierre #N"** al backlog del requerimiento (en la ficha de la historia en los Anexos, o una sección dedicada). Este registro es el contexto de entrada de las sesiones siguientes: antes de retomar un requerimiento se lee el backlog completo — tabla de estados + cierres.

Formato del bloque:

```markdown
### Cierre #N — YYYY-MM-DD

| Campo | Valor |
|---|---|
| Estado final | 🟣 PR #X (pendiente de merge) o ✅ merge |
| Sesiones | fecha: qué se hizo (duración estimada) · … |
| Tiempo total | estimado: timestamps de commits + duración de sesiones |
| Commits | hashes cortos con etiqueta (docs / backend / frontend / backlog) |
| Resumen | qué entrega la historia, en 2-4 líneas |
| Lecciones | contratos pisados, trampas del entorno, decisiones que costaron tiempo |
```

Notas:

- **El tiempo es una estimación declarada**, no una medición exacta: se deriva de los timestamps de los commits de la historia (primer → último) más la duración percibida de cada sesión. El humano puede corregir la cifra al revisar el backlog.
- La sección **Lecciones** es la memoria técnica del proyecto: evita re-pisar contratos (tests de contrato, snapshots, approvals) y documenta trampas del entorno (p. ej. tests que dependen del SO).
- En proyectos con skill de inicio de sesión (p. ej. `iniciar-sesion`), apuntarla a leer el backlog + cierres como primera fuente de contexto.

## 7. Adopción en un proyecto nuevo

1. Instalar las skills globalmente (ver README) — no requiere cambios en el proyecto.
2. Agregar al `AGENTS.md` del proyecto (una sola vez):
   - Los quality gates con sus comandos exactos (p. ej. `./entrypoint.sh lint && ./entrypoint.sh typecheck && ./entrypoint.sh test`).
   - El flujo de git (worktrees, branching, reglas de commit/PR).
   - Una línea apuntando a este método: `Modus operandi: /backlog → /story → /pair (ver fork hola-ai, MODUS_OPERANDI.md)`.
3. **Tracker de historias:** dos opciones válidas, elegir por proyecto:
   - **Backlog local `.md`** (recomendado para equipos pequeños): versionado junto al spec, tabla con columnas `#`, `Historia`, `Estado`, `Ref` (branch/PR) y `Requiere`. El `Estado` se actualiza al cierre de cada sesión de `/pair` (`⬜ pendiente → 🔵 /story → 🟠 /pair → 🟣 PR → ✅ merge`). El fichero del `/story` (criterios + plan) vive como anexo en el mismo `.md` o en un sub-archivo por historia.
   - **GitHub Issues / Jira** (recomendado si hay más personas o se necesita triage/CI): `/backlog` sube una issue por historia; `/story` arma el cuerpo del issue; el PR la cierra automáticamente (`closes #N`).
4. Opcional: etiqueta dedicada para las historias (p. ej. `story` o las etiquetas de triage existentes).

## 8. Antipatrones (lo que este método evita)

- Specs que producen tareas técnicas ("crear modelo X") en vez de valor de usuario.
- Dividir por capas (backend/UI) en vez de cortar verticalmente.
- La IA decidiendo arquitectura sin señal concreta en el código.
- Commits automáticos de la IA o refactors mezclados con funcionalidad.
- Abstracciones anticipadas "para el futuro".
- Correr quality gates solo al final: corren antes de cada commit propuesto.