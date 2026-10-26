---
name: story
description: Toma UNA historia de usuario del backlog, agrega 2-3 criterios de aceptación y propone un mini plan de implementación para aprobación. No escribe código; la implementación es trabajo de /pair.
disable-model-invocation: true
---

# Story

Refinamos una sola historia, justo antes de construirla. Tú propones y yo decido.

## Pasos

1. **Lee la historia** que te doy (texto pegado, issue de GitHub, ticket de Jira, etc.) y revisa el código actual y `AGENTS.md` para entender el contexto.
2. **Criterios de aceptación.** Propón 2–3 en formato Dado/Cuando/Entonces. Solo describen *qué* ve u obtiene el usuario, nunca *cómo* se implementa.
3. **Si necesita más de 3 criterios, no la infles: propone dividirla.** Entrega las nuevas historias en formato backlog (`Como…, quiero…, para…`) para que yo las agregue al tracker, y seguimos con la primera.
4. **Mini plan.** Máximo 5 bullets, sin código ni nombres de archivos. Cómo atraviesa las capas, con lo mínimo que cumple los criterios.
5. **Espera mi aprobación.** Ajustamos hasta que yo diga que sí.

## Reglas

- **No inventes requisitos.** Si falta información, pregúntame.
- **Lo más simple que cumpla los criterios.** Sin abstracciones, capas, configuración ni patrones "para el futuro".
- **Sugiere, no decidas.** Si un patrón podría ayudar (Atomic Design, composición de middleware, extraer un componente…), menciónalo en "Sugerencias" con su porqué. Solo sugiérelo si hay una señal concreta en el código (por ejemplo, algo que ya se repite), no por adelantado.
- **No escribas código.**

## Formato de salida

Un bloque listo para pegar en el issue. `/pair` lo usa como input.

```markdown
## Historia
Como <actor>, quiero <acción>, para <beneficio>.

## Criterios de aceptación
- [ ] Dado <contexto>, cuando <acción>, entonces <resultado>.
- [ ] ...

## Plan
- ...

## Fuera de alcance
- <lo que queda fuera de esta historia, para que no se cuele>

## Sugerencias (decides tú)
- <opcional>
```