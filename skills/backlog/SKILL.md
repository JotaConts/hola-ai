---
name: backlog
description: Convierte una idea de software o una funcionalidad discutida en un backlog de historias de usuario cortas y verticales. Sin criterios de aceptación ni implementación; eso es trabajo de /story.
disable-model-invocation: true
---

# Backlog

Tu trabajo es ayudarme a dividir lo que te cuento en historias de usuario. Yo traigo los requisitos; tú los ordenas y los troceas.

## Conversación

1. Escucha la idea o funcionalidad. Si algo no está claro, pregunta. Una pregunta a la vez, con tu respuesta sugerida.
2. Si es un proyecto nuevo, hablemos del stack. Solo el stack, no la arquitectura ni la implementación.
3. Pregunta si aplica alguna de estas decisiones caras de cambiar. Solo pregunta, no las diseñes:
   - Multi-tenant o multi-organización
   - Modelo de permisos o roles
   - Offline o sincronización
   - Multi-idioma o multi-moneda
4. Propón el backlog. Yo lo ajusto.

## Reglas

- **No inventes requisitos.** Solo divide lo que te dije. Si ves un hueco, pregúntame; no lo rellenes.
- **Cada historia entrega valor por sí sola** y atraviesa todas las capas (datos, backend, UI). Nunca dividas por capas.
- **Nada de historias técnicas.** El actor nunca es el desarrollador ni el sistema. "Configurar la base de datos" o "crear el modelo de usuario" no son historias; esa infraestructura se construye dentro de la primera historia que la necesite.
- **Pocas historias.** 10–15 máximo. Prefiero agregar que quitar.
- **Una línea por historia.** Sin criterios de aceptación, sin detalles técnicos, sin estimaciones ni prioridades.
- La primera historia es la más pequeña utilizable de punta a punta (walking skeleton).

## Formato de salida

```markdown
## Contexto
<una o dos líneas: qué es y para quién>
Stack: <lo que acordamos>
Decisiones caras: <las que aplican, o "ninguna">

## Backlog
1. Como <actor>, quiero <acción>, para <beneficio>.
2. Como <actor>, quiero <acción>, para <beneficio>. Requiere: #1
```

Agrega `Requiere: #N` solo cuando una historia no tiene sentido sin otra.

Al terminar, ofrece guardar el contexto y el stack en `AGENTS.md` (o `CLAUDE.md`). Las historias van a mi tracker; no las guardes en archivos salvo que yo lo pida.