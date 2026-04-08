# Practical UI — Reglas para IA

## meta
- domain: practical-ui
- source: "Practical UI — Adham Dannaway"
- goal: aplicar reglas binarias de “Sí vs No” sobre luz, sombras, profundidad y legibilidad

## dimensions_enabled
- elevation_and_shadows
- hierarchy_and_depth
- legibility
- accessibility

# 1. Elevation & shadows

check:
  - name: shadow_strength_vs_elevation
    target: ["card","modal","floating_button"]
    rule:
      - elevation_low AND shadow_blur_large & opacity_high -> issue
      - elevation_high AND shadow too subtle -> issue
    output_template:
      dimension: "elevation_and_shadows"
      problem: "Sombra no coherente con la elevación"
      recommendation_patterns:
        - "Usa sombras pequeñas y suaves para elementos cercanos al fondo, y más grandes/difusas para elementos flotantes"

  - name: multiple_light_sources
    target: ["screen"]
    rule:
      - inconsistent_shadow_directions -> issue
    output_template:
      dimension: "elevation_and_shadows"
      problem: "Sombras con múltiples direcciones (fuentes de luz inconsistentes)"
      recommendation_patterns:
        - "Alinea todas las sombras con una única fuente de luz (p.ej. arriba-izquierda)"

# 2. Hierarchy & depth

check:
  - name: depth_used_for_priority
    target: ["screen"]
    rule:
      - low_priority_elements_on_top_with_stronger_shadows -> issue
    output_template:
      dimension: "hierarchy_and_depth"
      problem: "Elementos secundarios parecen más “por encima” que los principales"
      recommendation_patterns:
        - "Reserva mayor elevación y sombras para contenido y acciones más importantes"

# 3. Legibility (legibilidad)

check:
  - name: minimum_font_size_mobile
    target: ["text_on_mobile"]
    rule:
      - role == "primary_text" AND font_size < 16px -> issue
      - role == "secondary_text" AND font_size < 12px -> issue
    output_template:
      dimension: "legibility"
      problem: "Tamaño de fuente insuficiente en mobile"
      recommendation_patterns:
        - "Usa mínimo 16px para texto primario en mobile; 12–14px para texto secundario"

  - name: text_on_images
    target: ["text_over_image"]
    rule:
      - low_contrast_with_background OR busy_background -> issue
    output_template:
      dimension: "legibility"
      problem: "Texto sobre imagen difícil de leer"
      recommendation_patterns:
        - "Añade overlay oscuro/claro, blur o caja sólida detrás del texto"

# 4. Accessibility

check:
  - name: hit_target_size
    target: ["button","icon_button","control"]
    rule:
      - touch_device AND size < 44x44 -> issue
    output_template:
      dimension: "accessibility"
      problem: "Área clicable demasiado pequeña"
      recommendation_patterns:
        - "Asegura que los objetivos táctiles midan al menos ~44×44 px"

  - name: secondary_text_weight
    target: ["secondary_text"]
    rule:
      - font_size_small AND color_low_contrast AND weight_thin -> issue
    output_template:
      dimension: "accessibility"
      problem: "Texto secundario excesivamente débil"
      recommendation_patterns:
        - "Equilibra tamaño, color y peso para que sea legible pero no compita con el primario"