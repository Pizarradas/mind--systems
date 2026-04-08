# Microinteractions (Dan Saffer) — Reglas para IA

## meta
- domain: microinteractions
- source: "Microinteractions: Designing with Details"
- goal: evaluar los pequeños detalles de interacción que mejoran la UX

## concepts_enabled
- triggers
- rules
- feedback
- loops_and_modes

# Triggers (disparadores)
check:
  - name: unclear_triggers
    target: ["microinteraction"]
    rule:
      - trigger_not_obvious OR trigger_distant_from_object -> issue
output_template:
  concept: "triggers"
  problem: "No está claro qué acción inicia la microinteracción"
  recommendation_patterns:
    - "Haz el disparador visible y cercano al elemento afectado"

# Rules (reglas de comportamiento)
check:
  - name: confusing_rules
    target: ["microinteraction"]
    rule:
      - system_response_inconsistent_with_trigger -> issue
output_template:
  concept: "rules"
  problem: "La respuesta del sistema no se entiende a partir de la acción"
  recommendation_patterns:
    - "Asegura que la consecuencia sea predecible y coherente con el disparador"

# Feedback
check:
  - name: micro_feedback_presence
    target: ["control","state_change"]
    rule:
      - no_micro_feedback (no subtle animation, color change, sound) -> warning
output_template:
  concept: "feedback"
  problem: "Falta feedback sutil al interactuar"
  recommendation_patterns:
    - "Añade pequeñas animaciones, cambios de color o microcopys para confirmar la acción"

# Loops & modes
check:
  - name: unclear_modes
    target: ["mode_toggle"]
    rule:
      - mode_change_not_visually_obvious -> issue
  - name: endless_loops
    target: ["repeated_notification","reminder"]
    rule:
      - loop_no_exit_or_adaptation -> issue
output_template:
  concept: "loops_and_modes"
  problem: "Modos no claros o loops molestos"
  recommendation_patterns:
    - "Haz visible en qué modo está el usuario"
    - "Limita repeticiones: adapta frecuencia o permite desactivar"

## micro_checklist
- ¿La acción que dispara el cambio es evidente?
- ¿La respuesta del sistema se entiende sin pensar?
- ¿Hay feedback sutil (no solo grandes mensajes)?
- ¿Los modos y estados persistentes se ven claramente?
- ¿Las notificaciones repetidas se controlan o adaptan?
