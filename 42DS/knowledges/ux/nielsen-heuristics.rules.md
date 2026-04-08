# 10 Usability Heuristics (Jakob Nielsen) — Reglas para IA

## meta
- domain: usability-heuristics
- source: "10 Usability Heuristics for User Interface Design — Jakob Nielsen"
- goal: evaluar interfaces según 10 heurísticas clásicas

## heuristics_enabled
- visibility_of_system_status
- match_between_system_and_real_world
- user_control_and_freedom
- consistency_and_standards
- error_prevention
- recognition_rather_than_recall
- flexibility_and_efficiency_of_use
- aesthetic_and_minimalist_design
- help_users_recognize_diagnose_recover_errors
- help_and_documentation

# 1. Visibilidad del estado del sistema
check:
  - name: action_feedback
    target: ["action"]
    rule:
      - time_to_feedback > 0.5s -> issue
  - name: system_status_presence
    target: ["screen"]
    rule:
      - long_process AND no_progress_indicator -> issue
output_template:
  heuristic: "visibility_of_system_status"
  problem: "Estado del sistema poco visible"
  recommendation_patterns:
    - "Muestra feedback inmediato tras cada acción (loaders, toasts, cambios de estado)"
    - "Usa barras de progreso o pasos claros en procesos largos"

# 2. Correspondencia sistema–mundo
check:
  - name: real_world_language
    target: ["labels","messages"]
    rule:
      - jargon_high AND audience != expert -> issue
  - name: natural_order
    target: ["forms","flows"]
    rule:
      - field_order != mental_model_order -> issue
output_template:
  heuristic: "match_between_system_and_real_world"
  problem: "Lenguaje u orden poco naturales para el usuario"
  recommendation_patterns:
    - "Usa palabras, metáforas y orden cercanos a la vida real del usuario"
    - "Reorganiza campos para seguir el orden mental habitual"

# 3. Control y libertad del usuario
check:
  - name: undo_redo_paths
    target: ["critical_action"]
    rule:
      - no_undo AND destructive == true -> issue
  - name: escape_routes
    target: ["modal","wizard"]
    rule:
      - no_cancel OR no_back -> issue
output_template:
  heuristic: "user_control_and_freedom"
  problem: "Falta de control o vías de escape para el usuario"
  recommendation_patterns:
    - "Añade deshacer/revertir para acciones destructivas"
    - "Incluye botones de Cancelar y Atrás en flujos multi-paso"

# 4. Consistencia y estándares
check:
  - name: visual_consistency
    target: ["screen"]
    rule:
      - inconsistent_styles_for_same_pattern -> issue
  - name: platform_conventions
    target: ["component"]
    rule:
      - deviates_platform_standard_without_reason -> issue
output_template:
  heuristic: "consistency_and_standards"
  problem: "Inconsistencias o ruptura de estándares"
  recommendation_patterns:
    - "Reutiliza patrones visuales y de interacción de forma consistente"
    - "Alinea componentes con las pautas de la plataforma (iOS, Android, web)"

# 5. Prevención de errores
check:
  - name: destructive_actions_protection
    target: ["destructive_action"]
    rule:
      - no_confirmation AND impact == high -> issue
  - name: constraints
    target: ["input"]
    rule:
      - no_validation AND error_likely -> issue
output_template:
  heuristic: "error_prevention"
  problem: "Errores fáciles de cometer"
  recommendation_patterns:
    - "Añade confirmaciones para acciones irreversibles"
    - "Valida y limita la entrada para evitar errores comunes"

# 6. Reconocimiento mejor que recuerdo
check:
  - name: recall_vs_recognition
    target: ["selection","navigation"]
    rule:
      - user_must_remember_id_or_code AND alternative_list_possible -> issue
output_template:
  heuristic: "recognition_rather_than_recall"
  problem: "Se exige recordar información que podría ser visible"
  recommendation_patterns:
    - "Sustituye campos de texto por listas, sugerencias o autocompletado"
    - "Muestra historial o elementos recientes"

# 7. Flexibilidad y eficiencia de uso
check:
  - name: accelerators_for_experts
    target: ["flow"]
    rule:
      - high_frequency AND no_shortcuts_for_power_users -> notice
output_template:
  heuristic: "flexibility_and_efficiency_of_use"
  problem: "Falta de atajos para usuarios frecuentes"
  recommendation_patterns:
    - "Añade atajos de teclado, saltos de paso o presets para expertos"

# 8. Diseño estético y minimalista
check:
  - name: visual_noise
    target: ["screen"]
    rule:
      - irrelevant_elements_ratio > threshold -> issue
output_template:
  heuristic: "aesthetic_and_minimalist_design"
  problem: "Demasiados elementos irrelevantes"
  recommendation_patterns:
    - "Elimina texto, iconos o elementos decorativos que no ayuden a la tarea"
    - "Simplifica la pantalla a lo esencial para el objetivo actual"

# 9. Ayudar a reconocer, diagnosticar y recuperarse de errores
check:
  - name: error_message_quality
    target: ["error_message"]
    rule:
      - only_generic_message OR no_next_step -> issue
output_template:
  heuristic: "help_users_recognize_diagnose_recover_errors"
  problem: "Mensajes de error poco útiles"
  recommendation_patterns:
    - "Explica qué pasó, por qué y qué puede hacer el usuario"
    - "Usa tono claro y no culpabilizador"

# 10. Ayuda y documentación
check:
  - name: help_availability
    target: ["complex_flow","advanced_feature"]
    rule:
      - complexity_high AND no_help_entry_point -> issue
output_template:
  heuristic: "help_and_documentation"
  problem: "Falta de ayuda accesible en tareas complejas"
  recommendation_patterns:
    - "Incluye enlaces a ayuda contextual o FAQ"
    - "Muestra tips breves en puntos críticos, sin saturar"
