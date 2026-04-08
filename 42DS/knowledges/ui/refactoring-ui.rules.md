# Refactoring UI — Reglas para IA

## meta
- domain: visual-design
- source: "Refactoring UI — Adam Wathan & Steve Schoger"
- goal: evaluar espaciado, color, tipografía y limpieza visual

## dimensions_enabled
- spacing
- typography
- color_and_contrast
- layout_and_hierarchy

# 1. Spacing (espaciado)

check:
  - name: consistent_vertical_rhythm
    target: ["stacked_elements"]
    rule:
      - spacing_between_items not in [4,8,12,16,20,24,32] (o escalas definidas) -> issue
    output_template:
      dimension: "spacing"
      problem: "Espaciado vertical inconsistente"
      recommendation_patterns:
        - "Ajusta el espacio entre elementos para que siga una escala consistente (4/8/12/16/24/32...)"

  - name: padding_consistency
    target: ["button","card","input"]
    rule:
      - padding_vertical / padding_horizontal fuera_de_rango [0.5,1] -> issue
    output_template:
      dimension: "spacing"
      problem: "Padding interno desproporcionado"
      recommendation_patterns:
        - "Usa padding vertical y horizontal basados en la misma escala para mantener proporción"

# 2. Typography (tipografía)

check:
  - name: hierarchy_levels
    target: ["text_styles"]
    rule:
      - heading_levels < 2 OR heading_levels > 4 -> warning
    output_template:
      dimension: "typography"
      problem: "Jerarquía tipográfica pobre o excesiva"
      recommendation_patterns:
        - "Define 2–4 niveles claros (H1/H2/H3 + body) y reutilízalos"

  - name: line_height_readability
    target: ["body_text"]
    rule:
      - line_height / font_size not in [1.3,1.6] -> issue
    output_template:
      dimension: "typography"
      problem: "Interlineado poco legible"
      recommendation_patterns:
        - "Ajusta el line-height a ~1.4–1.6 para párrafos"

# 3. Color & contrast

check:
  - name: dark_background_text_color
    target: ["text_on_dark_bg"]
    rule:
      - text_color == pure_white (#FFFFFF) AND bg_luminance_low -> warning
    output_template:
      dimension: "color_and_contrast"
      problem: "Texto blanco puro sobre fondo oscuro"
      recommendation_patterns:
        - "Usa un gris muy claro en lugar de blanco puro para reducir fatiga visual"

  - name: contrast_wcag
    target: ["text","icon"]
    rule:
      - contrast_ratio(text_color, bg_color) < 4.5 (para texto normal) -> issue
      - contrast_ratio < 3.0 (para texto grande / UI element secondary) -> issue
    output_template:
      dimension: "color_and_contrast"
      problem: "Contraste insuficiente según WCAG"
      recommendation_patterns:
        - "Ajusta color de texto o fondo hasta alcanzar un ratio ≥ 4.5:1 para texto normal"

# 4. Layout & hierarchy

check:
  - name: noisy_cards
    target: ["card"]
    rule:
      - too_many_borders OR too_many_dividers -> issue
    output_template:
      dimension: "layout_and_hierarchy"
      problem: "Exceso de líneas/bordes para separar contenido"
      recommendation_patterns:
        - "Usa espacios, tamaño de texto y color para separar, en lugar de demasiadas líneas"

  - name: focal_point
    target: ["screen"]
    rule:
      - no_clear_primary_visual_weight -> issue
    output_template:
      dimension: "layout_and_hierarchy"
      problem: "Falta un punto focal claro"
      recommendation_patterns:
        - "Aumenta tamaño, contraste o proximidad del elemento principal y reduce ruido alrededor"

## high_level_checklist
- ¿El espaciado sigue una escala repetible?
- ¿Los componentes comparten patrones de padding?
- ¿La jerarquía tipográfica es clara (2–4 niveles)?
- ¿El texto en fondos oscuros usa grises claros, no blanco puro?
- ¿El contraste cumple ratios WCAG mínimos?