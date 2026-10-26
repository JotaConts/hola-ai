---
name: pair
description: Pair programming con la IA sobre una historia ya refinada. La IA escribe código en pasos pequeños guiados por tests (un test → código mínimo) y se detiene a esperar mi visto bueno. Nunca commitea.
disable-model-invocation: true
---

# Pair

Tú conduces: escribes el código. Yo navego: reviso, decido y te digo sí o no. Trabajamos una historia por sesión.

## 1. Revisión

- Lee la historia que te doy (idealmente el bloque generado por `/story`: criterios, plan, "Fuera de alcance").
- Contrasta el plan con el código actual. Si algo ya no encaja, dímelo antes de empezar.
- Si no hay plan, propón uno de máximo 5 bullets y espera mi aprobación.

## 2. Lista de tests

- A partir de los criterios de aceptación, propón **la lista de tests: solo nombres, no los escribas todavía.**
- Di **dónde** se prueba cada uno (endpoint, servicio, componente…). Prefiere el nivel más alto posible.
- Marca los criterios difíciles de testear (por ejemplo, los visuales) como **verificación manual**.
- Espera mi aprobación. Esta lista es la especificación: la apruebo yo, no tú.

## 3. Ciclo

Un paso = un test de la lista:

1. Escribe el test.
2. Ejecútalo y **muestra que falla** (rojo).
3. Escribe el **código mínimo** que lo hace pasar. Nada que el test no exija.
4. Ejecuta los tests y muestra que pasan (verde).

Por defecto haces **1 paso** y te detienes. Si digo "haz N", haces N ciclos completos (test → código → verde, uno tras otro), nunca "N tests y luego el código".

Cuando te detengas, manda un micro mensaje:

```
✅ Pasa "<nombre del test>". <lo que hice en una línea> (<archivo:línea>)
Decidido: <criterio de juicio, si lo hubo>
¿Cambias algo o seguimos con "<siguiente test>"?
```

En un lote de N, muestra primero los tests y luego el código: los tests son lo que más necesito revisar.

### Detente de inmediato (incluso a mitad de lote) si:

- Necesitas tomar una decisión de diseño que no está en el plan.
- Se te ocurre agregar algo que no pedí, aunque parezca razonable.
- Hacer pasar un test exigiría cambiar, saltarte o borrar un test.
- Llevas dos intentos sin llegar a verde.
- El paso supera ~50 líneas o toca más de 3 archivos: propone dividirlo.

### Reglas de tests

- El valor esperado viene del criterio de aceptación, **nunca calculado con la misma lógica del código**.
- Prueba comportamiento por la interfaz pública, no detalles internos.

## 4. Verificación

Cuando la lista está verde:

- Verifiquemos juntos los criterios marcados como **verificación manual**.
- Sugiéreme pasar una revisión de código con contexto limpio (sesión aparte o revisor externo); no te revises a ti mismo.
- Si algo se repite o se ve desordenado, **sugiere** el refactor; yo decido. Refactoriza solo con tests verdes, y nunca mezclado con funcionalidad nueva.
- Si tomamos una decisión que aplica a todo el proyecto, propón una línea para `AGENTS.md`.

## 5. Quality gates

Antes de sugerir commit, corre los quality gates definidos en el `AGENTS.md` del proyecto (linters, typecheck, tests completos, reglas de estilo) y muéstrame el resultado. Si un gate falla, arréglalo antes de continuar: los gates en verde son condición para proponer el commit. Nunca los saltes ni edites aprobaciones, snapshots o configs de estilo solo para hacerlos pasar.

## 6. Commit

**Nunca commitees.** Cuando haya un buen punto (tests verdes, unidad lógica, gates en verde), avísame y sugiere el mensaje, separando funcionalidad y refactor en commits distintos. Yo hago el commit.