# Motion & Microinteractions in UI — Reglas para IA

## meta
- domain: ui
- subdomain: motion-and-microinteractions
- sources:
  - Microinteractions (Dan Saffer), Material Design Motion, Apple HIG Animation
- goal: evaluar animaciones y microinteracciones desde la UI (no código)

## dimensions_enabled
- purpose
- timing_and_easing
- continuity
- accessibility_motion

# 1. Propósito (purpose)

check:
  - name: motion_has_purpose
    target: ["animation","microinteraction"]
    rule:
      - role not in ["feedback","state_change","navigation_transition","attention_hint"]
        -> warning
    output_template:
      dimension: "purpose"
      problem: "Animación sin propósito claro"
      recommendation_patterns:
        - "Usa animación para feedback, transiciones, jerarquía o estado; evita decoraciones gratuitas"

# 2. Timing & easing

## Rangos típicos (inspirados en Material/HIG):
## - microinteracciones: 150–250 ms
## - transiciones de navegación: 200–400 ms

check:
  - name: duration_range
    target: ["animation"]
    rule:
      - duration_ms < 100 OR duration_ms > 500 -> warning
    output_template:
      dimension: "timing_and_easing"
      problem: "Duración de animación fuera de rango común"
      recommendation_patterns:
        - "Ajusta microinteracciones a ~150–250 ms; transiciones a ~200–400 ms"

  - name: easing_curve
    target: ["animation"]
    rule:
      - easing_type in ["linear"] AND context != "constant_motion" -> warning
    output_template:
      dimension: "timing_and_easing"
      problem: "Curva de easing poco natural (lineal)"
      recommendation_patterns:
        - "Usa curvas de aceleración/desaceleración (ease-in-out, standard curve de Material)"

# 3. Continuidad (continuity)

check:
  - name: element_continuity_between_screens
    target: ["navigation_transition"]
    rule:
      - element_reappears_in_new_screen_but_no_motion_link -> notice
    output_template:
      dimension: "continuity"
      problem: "Transición sin relación visual entre origen y destino"
      recommendation_patterns:
        - "Usa motion para indicar que es el mismo elemento (shared element transition, scale, position)"

  - name: motion_overload
    target: ["screen"]
    rule:
      - animated_elements_count > threshold -> warning
    output_template:
      dimension: "continuity"
      problem: "Demasiados elementos animados a la vez"
      recommendation_patterns:
        - "Reduce el número de elementos en movimiento simultáneo para no saturar al usuario"

# 4. Accesibilidad (accessibility_motion)

check:
  - name: respects_reduce_motion
    target: ["animation"]
    rule:
      - system_setting_reduce_motion == true AND animation_not_simplified -> issue
    output_template:
      dimension: "accessibility_motion"
      problem: "Animaciones no respetan la preferencia de reducir movimiento"
      recommendation_patterns:
        - "Proporciona versiones más sutiles o desactiva animaciones no esenciales cuando ‘reduce motion’ está activo"

  - name: potential_motion_sickness
    target: ["animation"]
    rule:
      - large_area_motion AND repeated_loop -> warning
    output_template:
      dimension: "accessibility_motion"
      problem: "Animación de gran área y bucle constante puede provocar mareo"
      recommendation_patterns:
        - "Limita loops, reduce amplitud del movimiento o hazlo opcional"

## microinteractions_structure_reminder
- Toda microinteracción puede describirse como:
  - trigger (qué la inicia)
  - rules (qué pasa)
  - feedback (qué ve/oye/siente el usuario)
  - loops & modes (cómo se repite o cambia con el tiempo)