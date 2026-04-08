# About Face (Alan Cooper) — Reglas para IA

## meta
- domain: interaction-design-goal-directed
- source: "About Face: The Essentials of Interaction Design"
- goal: diseñar y evaluar flujos orientados a objetivos y modelos mentales

## concepts_enabled
- personas_and_goals
- goal_directed_flows
- posture_of_products
- dialogs_vs_direct_manipulation

# Personas y objetivos
check:
  - name: goal_alignment
    target: ["flow","screen"]
    rule:
      - no_clear_user_goal OR ui_elements_not_supporting_primary_goal -> issue
output_template:
  concept: "personas_and_goals"
  problem: "La interfaz no está claramente alineada con un objetivo del usuario"
  recommendation_patterns:
    - "Explicita el objetivo principal del usuario y elimina elementos que no contribuyen a él"

# Flujos orientados a objetivos
check:
  - name: goal_first_flow
    target: ["flow"]
    rule:
      - many_low_value_steps_before_core_goal -> issue
output_template:
  concept: "goal_directed_flows"
  problem: "Demasiados pasos previos antes de aportar valor"
  recommendation_patterns:
    - "Acerca la ‘primera victoria’ del usuario al principio del flujo"
    - "Retrasa datos secundarios para después de lograr el objetivo principal"

# Postura del producto (sovereign, transient, daemonic)
check:
  - name: posture_mismatch
    target: ["app"]
    rule:
      - product_usage_pattern != ui_posture -> issue
output_template:
  concept: "posture_of_products"
  problem: "La interfaz no coincide con la frecuencia/intensidad de uso"
  recommendation_patterns:
    - "Apps usadas continuamente: UI más densa y eficiente"
    - "Apps usadas ocasionalmente: UI más guiada y simple"

# Diálogos vs manipulación directa
check:
  - name: overuse_of_dialogs
    target: ["screen"]
    rule:
      - many_modals_for_simple_actions -> issue
output_template:
  concept: "dialogs_vs_direct_manipulation"
  problem: "Demasiados diálogos donde se podría usar manipulación directa"
  recommendation_patterns:
    - "Permite que el usuario actúe directamente sobre los objetos (arrastrar, editar in-place) en lugar de diálogos innecesarios"

## high_level_checklist
- ¿Está claro qué persona/rol está usando esta pantalla?
- ¿Qué objetivo principal tiene aquí y cuántos pasos hasta lograrlo?
- ¿La “primera victoria” llega pronto?
- ¿La densidad de la UI coincide con la frecuencia de uso?
