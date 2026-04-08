# knowledge/ux — Índice del dominio

## Propósito
Conocimientos de UX agnósticos a proyecto. Fuente de verdad para agentes que toman decisiones sobre usabilidad, flujos, copy e interacción.

---

## Archivos del dominio

| Archivo | Tema | agent_tags |
|---|---|---|
| `laws-of-ux.md` | Leyes psicológicas de UX (Hick, Fitts, Miller, Jakob, Estética) | ux, audit, flow |
| `nielsen-heuristics.md` | 10 heurísticas clásicas de usabilidad | ux, audit, ui |
| `dont-make-me-think.md` | Claridad, escaneo, satisficing, happy path | ux, audit, flow |
| `design-of-everyday-things.md` | Affordances, signifiers, mapeo, feedback, estados | ux, audit, ui |
| `about-face.md` | Diseño orientado a objetivos, postura del producto, manipulación directa | ux, flow, audit |
| `100-things-people.md` | Percepción, atención, memoria, motivación (psicología aplicada) | ux, audit, flow |
| `strategic-writing-for-ux.md` | Microcopy, botones, errores, empty states, títulos | ux, copy, audit |
| `microinteractions.md` | Triggers, rules, feedback sutil, loops y modos | ux, ui, audit |
| `service-design-thinking.md` | Experiencia end-to-end, touchpoints, blueprint, canales | ux, flow, audit |
| `lean-ux-and-metrics.md` | Hipótesis, experimentos, métricas de UX | ux, flow, audit |

---

## Carga recomendada por agente

| Agente | Archivos a cargar |
|---|---|
| Agente UX (auditoría general) | todos |
| Agente de flujos / flows | `laws-of-ux`, `about-face`, `dont-make-me-think`, `service-design-thinking`, `lean-ux-and-metrics` |
| Agente de copy / UX writing | `strategic-writing-for-ux`, `dont-make-me-think`, `100-things-people` |
| Agente de interacción / microUX | `design-of-everyday-things`, `microinteractions`, `nielsen-heuristics` |
| Agente de métricas / producto | `lean-ux-and-metrics`, `laws-of-ux` |

---

## Estructura interna de cada archivo

Todos los archivos del dominio siguen esta estructura:

```
## meta          → dominio, fuente, objetivo, agent_tags
## concepts      → marco conceptual mínimo para razonar en casos ambiguos
## rules         → reglas operativas con checks, targets y recommendations
## checklist     → preguntas de validación rápida
```
