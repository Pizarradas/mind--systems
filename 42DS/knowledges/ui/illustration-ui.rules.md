# Illustration in UI — Reglas para IA

## meta
- domain: ui
- subdomain: illustration
- sources:
  - Tubik, Nick Babich, Shakuro, Dizz Agency (best practices ilustración UI)
- goal: evaluar cuándo, cómo y cuánto usar ilustraciones en producto digital

## dimensions_enabled
- purpose
- style_consistency
- hierarchy_and_focus
- accessibility

# 1. Propósito (purpose)

check:
  - name: illustration_has_purpose
    target: ["illustration"]
    rule:
      - context in ["onboarding","empty_state","error_state","hero","education"]
        AND meaning == "pure_decoration"
        -> warning
    output_template:
      dimension: "purpose"
      problem: "Ilustración sin propósito claro"
      recommendation_patterns:
        - "Usa ilustraciones para explicar, reforzar el mensaje o generar confianza"
        - "Evita ilustraciones puramente decorativas en zonas críticas de tarea"

  - name: illustration_vs_text_balance
    target: ["screen"]
    rule:
      - large_illustration AND critical_task_elements_pushed_below_fold -> issue
    output_template:
      dimension: "purpose"
      problem: "Ilustración compite con la tarea principal"
      recommendation_patterns:
        - "Reduce tamaño o reubica la ilustración para que la acción principal siga siendo protagonista"

# 2. Estilo y consistencia (style_consistency)

check:
  - name: style_alignment
    target: ["illustration_set"]
    rule:
      - mixed_styles (flat + skeuomorphic + outline, etc.) -> warning
    output_template:
      dimension: "style_consistency"
      problem: "Estilos de ilustración mezclados"
      recommendation_patterns:
        - "Define 1 estilo ilustrativo (flat, outline, duotone, etc.) y mantenlo consistente"

  - name: palette_alignment
    target: ["illustration"]
    rule:
      - illustration_palette not_compatible_with_ui_palette -> issue
    output_template:
      dimension: "style_consistency"
      problem: "Paleta de color de ilustración no alineada con la UI"
      recommendation_patterns:
        - "Reusa los colores del sistema (accent, neutrals) o variaciones compatibles"

# 3. Jerarquía y foco (hierarchy_and_focus)

check:
  - name: illustration_dominance
    target: ["screen"]
    rule:
      - illustration_visual_weight > primary_cta_visual_weight AND context == "task_flow" -> warning
    output_template:
      dimension: "hierarchy_and_focus"
      problem: "La ilustración domina sobre el CTA en un flujo de tarea"
      recommendation_patterns:
        - "Reduce contraste/tamaño de la ilustración o incrementa el peso visual del CTA"

# 4. Accesibilidad (accessibility)

check:
  - name: illustration_not_critical_for_understanding
    target: ["screen"]
    rule:
      - key_information_only_in_illustration -> issue
    output_template:
      dimension: "accessibility"
      problem: "Información crítica comunicada solo mediante ilustración"
      recommendation_patterns:
        - "Asegura que el mensaje principal también está en texto"

  - name: motion_in_illustrations
    target: ["animated_illustration"]
    rule:
      - high_motion AND context == "background" -> warning
    output_template:
      dimension: "accessibility"
      problem: "Ilustración animada potencialmente distractora"
      recommendation_patterns:
        - "Limita la animación de fondo o permite desactivarla"