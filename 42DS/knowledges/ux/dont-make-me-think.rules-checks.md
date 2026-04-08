# Don’t Make Me Think — Reglas para IA

## meta
- domain: usability
- source: "Don’t Make Me Think — Steve Krug"
- goal: minimizar fricción y carga cognitiva

## principles_enabled
- Clarity
- Scanability
- Satisficing
- Conventions
- HappyPath

## clarity
check:
  - name: page_purpose_clarity
    target: ["screen"]
    rule:
      - time_to_understand_purpose > 3s OR top_level_text_missing -> issue
    output_template:
      principle: "Clarity"
      problem: "Propósito de la pantalla no evidente"
      recommendation_patterns:
        - "Añade un título claro que resuma la tarea principal"
        - "Refuerza con subtítulo que explique qué obtiene el usuario"
  - name: primary_action_visibility
    target: ["screen"]
    rule:
      - primary_cta_missing OR primary_cta_visual_weight < secondary_elements -> issue
    output_template:
      principle: "Clarity"
      problem: "Acción principal no evidente"
      recommendation_patterns:
        - "Aumenta contraste, tamaño o posición del CTA principal"
        - "Reduce protagonismo de acciones secundarias"

## scanability
check:
  - name: text_blocks
    target: ["text_block"]
    rule:
      - chars_length > 400 AND no_headings_or_bullets -> issue
    output_template:
      principle: "Scanability"
      problem: "Texto difícil de escanear"
      recommendation_patterns:
        - "Divide en párrafos cortos con títulos y bullets"
        - "Destaca palabras clave relacionadas con la tarea"

## satisficing
check:
  - name: first_attention_target
    target: ["screen"]
    rule:
      - visual_first_focus != primary_goal_component -> issue
    output_template:
      principle: "Satisficing"
      problem: "Lo que más destaca no es lo que más conviene"
      recommendation_patterns:
        - "Reordena jerarquía visual para que el camino recomendado sea el más visible"

## conventions
check:
  - name: basic_ui_conventions
    target: ["links", "buttons", "nav"]
    rule:
      - inconsistent_link_styles OR unexpected_nav_location -> issue
    output_template:
      principle: "Conventions"
      problem: "Ruptura de convenciones que aumenta la duda"
      recommendation_patterns:
        - "Unifica estilo de enlaces y botones"
        - "Usa patrones de navegación comunes"

## happy_path
check:
  - name: happy_path_visibility
    target: ["screen"]
    rule:
      - steps_to_goal.hidden OR main_flow_cta_nested_in_hidden_menu -> issue
    output_template:
      principle: "HappyPath"
      problem: "Ruta principal poco visible"
      recommendation_patterns:
        - "Surfacea el flujo principal en la vista inicial"
        - "Evita esconder la acción crítica en menús secundarios"

## quick_yes_no_checklist
- Q1: propósito_claro_en_1_frase? (sí/no)
- Q2: siguiente_paso_obvio? (sí/no)
- Q3: elementos_parecen_clickables_sin_serlo? (sí/no)
- Q4: hay_ruido_visual_innecesario? (sí/no)
- Q5: ruta_feliz_visible_sin_hacer_scroll? (sí/no)
