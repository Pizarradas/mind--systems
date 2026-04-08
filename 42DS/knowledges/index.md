# knowledge/ — Índice global

## Propósito
Sistema de conocimiento agnóstico a proyecto. Fuente de verdad compartida para agentes de diseño de producto digital.

Cada agente carga únicamente los módulos relevantes para su tarea. Ni más, ni menos.

---

## Estructura del sistema

```
knowledge/
  ux/     → Usabilidad, flujos, copy, psicología, métricas
  ui/     → Visual, color, tipografía, motion, plataforma, imágenes
```

---

## Dominios

### /ux — 10 módulos
Conocimientos sobre cómo el usuario piensa, decide y se mueve por el producto.

| Módulo | Tema central | agent_tags |
|---|---|---|
| `laws-of-ux` | Hick, Fitts, Miller, Jakob, Estética | ux, audit, flow |
| `nielsen-heuristics` | 10 heurísticas clásicas de usabilidad | ux, audit, ui |
| `dont-make-me-think` | Claridad, escaneo, satisficing, happy path | ux, audit, flow |
| `design-of-everyday-things` | Affordances, signifiers, mapeo, feedback, estados | ux, audit, ui |
| `about-face` | Objetivos, postura del producto, manipulación directa | ux, flow, audit |
| `100-things-people` | Percepción, atención, memoria, motivación | ux, audit, flow |
| `strategic-writing-for-ux` | Microcopy, botones, errores, empty states | ux, copy, audit |
| `microinteractions` | Triggers, rules, feedback sutil, loops, modos | ux, ui, audit |
| `service-design-thinking` | Experiencia end-to-end, touchpoints, blueprint | ux, flow, audit |
| `lean-ux-and-metrics` | Hipótesis, experimentos, métricas de UX | ux, flow, audit |

→ Ver detalle de carga por agente en `/ux/index.md`

---

### /ui — 7 módulos
Conocimientos sobre cómo se construye y evalúa la capa visual del producto.

| Módulo | Tema central | agent_tags |
|---|---|---|
| `refactoring-ui` | Espaciado, tipografía, color, jerarquía visual | ui, audit |
| `practical-ui` | Sombras, elevación, legibilidad, accesibilidad táctil | ui, audit |
| `color-theory` | Paleta, hue shifting, contraste WCAG | ui, audit |
| `platform-guidelines` | Patrones iOS (HIG) y Android (Material Design 3) | ui, audit |
| `motion-microinteractions` | Animaciones, timing, easing, reduce motion | ui, audit |
| `illustration` | Uso, estilo, jerarquía y accesibilidad de ilustración | ui, audit |
| `images` | Fotografía, contraste, rendimiento, crops responsivos | ui, audit |

→ Ver detalle de carga por agente en `/ui/index.md`

---

## Carga por tipo de agente

| Agente | Dominios | Módulos clave |
|---|---|---|
| Agente UX completo | /ux | todos |
| Agente UI completo | /ui | todos |
| Agente de auditoría full-stack | /ux + /ui | todos |
| Agente de flujos | /ux | `laws-of-ux`, `about-face`, `dont-make-me-think`, `service-design-thinking`, `lean-ux-and-metrics` |
| Agente de copy | /ux | `strategic-writing-for-ux`, `dont-make-me-think`, `100-things-people` |
| Agente de interacción | /ux + /ui | `design-of-everyday-things`, `microinteractions`, `nielsen-heuristics`, `motion-microinteractions` |
| Agente de color | /ui | `color-theory`, `refactoring-ui` |
| Agente de accesibilidad | /ui | `practical-ui`, `color-theory`, `motion-microinteractions` |
| Agente de plataforma | /ui | `platform-guidelines`, `practical-ui` |
| Agente de métricas / producto | /ux | `lean-ux-and-metrics`, `laws-of-ux` |

---

## Relaciones entre dominios

Algunos módulos de `/ui` y `/ux` son complementarios. Cuando un agente trabaja en la intersección, debe cargar ambos:

| /ux | /ui | Intersección |
|---|---|---|
| `microinteractions` | `motion-microinteractions` | Feedback visual y animación |
| `design-of-everyday-things` | `practical-ui` | Affordances y estados visuales |
| `laws-of-ux` → Jakob | `platform-guidelines` | Convenciones de plataforma |
| `100-things-people` | `color-theory` | Atención, percepción y color |
| `nielsen-heuristics` | `refactoring-ui` | Consistencia visual y estándares |

---

## Estructura interna de cada módulo

Todos los módulos del sistema siguen esta estructura fija:

```
## meta          → dominio, fuente, objetivo, agent_tags
## concepts      → marco conceptual mínimo para razonar en casos ambiguos
## rules         → reglas operativas con checks, targets y recommendations
## checklist     → preguntas de validación rápida
```

---

## Convenciones del sistema

- **agent_tags** — etiquetas que determinan qué agente carga cada módulo.
- **concepts** — solo lo necesario para razonar en casos no cubiertos por las reglas.
- **rules** — operativas, con formato `check / target / rule / output`.
- **checklist** — preguntas binarias de validación rápida al final de cada módulo.
- Ningún módulo duplica contenido de otro. Si dos módulos se solapan, se referencia, no se repite.
