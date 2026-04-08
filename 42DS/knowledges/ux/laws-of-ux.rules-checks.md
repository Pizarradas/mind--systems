# Laws of UX — Reglas para IA

## meta
- domain: ui-ux-psychology
- source: "Laws of UX — Jon Yablonski"
- goal: evaluar interfaces según leyes psicológicas de UX

## laws_enabled
- Hick
- Fitts
- Miller
- AestheticUsability
- Jakob

## law.Hick
check:
  - name: count_visible_choices
    target: ["nav_menu", "choice_group", "filter_group"]
    rule:
      - count(options.visible) > 7 -> issue
    output_template:
      law: "Hick"
      problem: "Demasiadas opciones simultáneas"
      rationale: "Más opciones => mayor tiempo de decisión"
      recommendation_patterns:
        - "Agrupa opciones en categorías y deja visibles solo las principales (5–7)"
        - "Introduce filtros progresivos o pasos secuenciales"

## law.Fitts
check:
  - name: tappable_size
    target: ["button", "icon_button", "touch_target"]
    rule:
      - size.px_width < 44 OR size.px_height < 44 -> issue
    output_template:
      law: "Fitts"
      problem: "Objetivo demasiado pequeño"
      rationale: "Mayor precisión requerida => peor usabilidad"
      recommendation_patterns:
        - "Aumenta el área clicable al menos a ~44×44 px en dispositivos táctiles"
  - name: distance_to_related_content
    target: ["primary_cta"]
    rule:
      - distance_to(content.related) > threshold.large -> issue
    output_template:
      law: "Fitts"
      problem: "Botón demasiado alejado del contenido al que afecta"
      recommendation_patterns:
        - "Acerca el botón al elemento que modifica o agrúpalos visualmente"

## law.Miller
check:
  - name: long_lists
    target: ["menu", "list", "form_section"]
    rule:
      - count(items) > 9 -> issue
    output_template:
      law: "Miller"
      problem: "Demasiados ítems en un solo bloque"
      rationale: "La memoria de trabajo maneja ~7±2 elementos"
      recommendation_patterns:
        - "Agrupa ítems en bloques temáticos con títulos claros"
        - "Divide formularios en secciones/steps de 4–7 campos"

## law.AestheticUsability
check:
  - name: visual_consistency
    target: ["screen"]
    rule:
      - inconsistency(alignment, spacing, typography, color) == true -> issue
    output_template:
      law: "AestheticUsability"
      problem: "Inconsistencias visuales"
      rationale: "La estética influye en la percepción de usabilidad"
      recommendation_patterns:
        - "Unifica tipografías, tamaños, espaciados y estilos de botón"
  - name: beauty_masking_problems
    target: ["screen"]
    rule:
      - design_score.visual_high AND ux_issues_count.high -> notice
    output_template:
      law: "AestheticUsability"
      problem: "Diseño atractivo oculta problemas de usabilidad"
      recommendation_patterns:
        - "No confíes solo en la estética; reduce opciones y simplifica flujos"

## law.Jakob
check:
  - name: common_patterns
    target: ["header", "nav", "icon_set"]
    rule:
      - violates_conventions(global_patterns) == true -> issue
    examples_conventions:
      - logo_click -> home
      - cart_icon -> top_right
      - hamburger_menu -> top_left_or_right_mobile
    output_template:
      law: "Jakob"
      problem: "Ruptura de patrones conocidos sin beneficio claro"
      rationale: "Los usuarios esperan que tu producto funcione como los que ya conocen"
      recommendation_patterns:
        - "Alinea la posición y comportamiento con patrones estándar"
        - "Solo innova cuando el beneficio es evidente y educas al usuario"

## severity_rules
- law in [Hick, Fitts, Miller] AND location in ["checkout", "login", "critical_flow"] -> impact: high
- law == Jakob AND pattern_deviation_minor -> impact: low
- AestheticUsability inconsistencies -> impact: medium
