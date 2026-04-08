# Service Design Thinking — Reglas para IA

## meta
- domain: service-design
- source: "This Is Service Design Thinking/Doing"
- goal: evaluar experiencias end-to-end más allá de la pantalla

## concepts_enabled
- service_blueprint
- touchpoints
- frontstage_backstage
- consistency_across_channels

# Service blueprint
check:
  - name: missing_steps_outside_ui
    target: ["journey"]
    rule:
      - critical_steps_offscreen_ignored -> issue
output_template:
  concept: "service_blueprint"
  problem: "La experiencia considera solo la UI, no las interacciones fuera de ella"
  recommendation_patterns:
    - "Identifica pasos previos y posteriores (emails, soporte, procesos internos) y alinéalos con la UI"

# Touchpoints
check:
  - name: touchpoint_consistency
    target: ["email","web","app","support"]
    rule:
      - messaging_or_brand_inconsistent -> issue
output_template:
  concept: "touchpoints"
  problem: "Inconsistencia entre distintos puntos de contacto"
  recommendation_patterns:
    - "Unifica tono, mensajes clave y promesas entre canales"

# Frontstage / Backstage
check:
  - name: backend_constraints_visibility
    target: ["flow"]
    rule:
      - backend_limitations_affect_user AND no_explanation_or_mitigation -> issue
output_template:
  concept: "frontstage_backstage"
  problem: "Limitaciones internas impactan negativamente sin gestionarse en la experiencia"
  recommendation_patterns:
    - "Diseña mensajes y alternativas que amortigüen límites técnicos u operativos"

## high_level_checklist
- ¿La experiencia descrita tiene en cuenta antes/durante/después de la UI?
- ¿Los mensajes son coherentes entre canales?
- ¿Las restricciones internas están gestionadas desde el diseño de servicio?
