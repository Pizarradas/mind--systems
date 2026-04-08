# Lean UX + Métricas de UX — Reglas para IA

## meta
- domain: product-process-and-metrics
- source: "Lean UX" + "Measuring the User Experience"
- goal: conectar hallazgos de UX con hipótesis, experimentos y métricas

## concepts_enabled
- hypotheses
- experiments
- ux_outcomes
- ux_metrics

# Hipótesis (Lean UX)
template_hypothesis:
  - "Creemos que [este cambio] resultará en [este impacto] para [este usuario]. Sabremos que funciona cuando veamos [esta métrica] cambiar."

check:
  - name: missing_hypothesis
    target: ["proposal","design_change"]
    rule:
      - no_explicit_hypothesis -> notice
output_template:
  concept: "hypotheses"
  problem: "Cambio de diseño sin hipótesis explícita"
  recommendation_patterns:
    - "Formula una hipótesis con usuario objetivo, cambio esperado y métrica de validación"

# Experimentos
check:
  - name: opportunity_for_experiment
    target: ["high_impact_issue"]
    rule:
      - fix_has_multiple_options -> suggestion
output_template:
  concept: "experiments"
  problem: "Mejora potencial que se puede testear"
  recommendation_patterns:
    - "Plantea un experimento A/B para comparar las opciones de diseño"
    - "Define duración, segmento de usuarios y métrica principal"

# Resultados de UX (outcomes)
ux_outcomes_examples:
  - mejorar_tasa_de_éxito_de_tarea
  - reducir_tiempo_de_tarea
  - reducir_errores
  - aumentar_retención
  - aumentar_satisfacción

check:
  - name: outcome_alignment
    target: ["issue"]
    rule:
      - no_outcome_linked -> notice

# Métricas de UX
ux_metrics:
  - task_success_rate
  - time_on_task
  - error_rate
  - completion_rate
  - system_usability_scale (SUS)
  - customer_satisfaction (CSAT)
  - net_promoter_score (NPS)

check:
  - name: suggest_metrics_for_issue
    target: ["issue"]
    rule:
      - map(issue_type) -> recommended_metrics
output_template:
  concept: "ux_metrics"
  recommendation_patterns:
    - "Para problemas de encontrabilidad, mide task_success_rate y time_on_task"
    - "Para problemas de errores, mide error_rate y tasa de recuperación"
    - "Para cambios globales de usabilidad, mide SUS o CSAT"
    - "Para impacto global en producto, monitoriza NPS"

## metrics_mapping_examples
- issue_type: "navegación confusa"
  suggested_metrics: ["task_success_rate","time_on_task","error_rate"]
- issue_type: "flujos largos"
  suggested_metrics: ["completion_rate","dropoff_rate_por_paso"]
- issue_type: "percepción_general_de_usabilidad"
  suggested_metrics: ["SUS","CSAT"]
