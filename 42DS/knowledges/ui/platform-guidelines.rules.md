# Human Interface Guidelines (Apple) & Material Design 3 (Google) — Reglas para IA

## meta
- domain: platform-guidelines
- source: "Apple HIG" + "Material Design 3"
- goal: validar que la UI respeta patrones y estándares de iOS / Android / Web

## platforms_enabled
- ios
- android
- web_material

# 1. Navigation patterns

check:
  - name: ios_nav_structure
    target: ["app_ios"]
    rule:
      - root_level > 5_tabs -> issue
      - using_hamburger_for_primary_nav_on_ios -> warning
    output_template:
      platform: "ios"
      problem: "Patrón de navegación poco alineado con HIG"
      recommendation_patterns:
        - "Usa tab bar para secciones principales (hasta 5 tabs)"
        - "Evita el uso de hamburguer como navegación primaria en iOS si puedes"

  - name: android_nav_structure
    target: ["app_android"]
    rule:
      - tabs_in_top_bar AND too_many_tabs -> issue
      - no_bottom_nav_when_many_top_level_destinations -> warning
    output_template:
      platform: "android"
      problem: "Navegación inconsistente con Material"
      recommendation_patterns:
        - "Usa bottom navigation para 3–5 destinos principales"
        - "Lleva destinos secundarios al drawer"

# 2. Components usage

check:
  - name: ios_components
    target: ["app_ios"]
    rule:
      - using_material_only_patterns (FAB, extended FAB) without_reason -> warning
    output_template:
      platform: "ios"
      problem: "Patrones visuales más propios de otra plataforma"
      recommendation_patterns:
        - "Adapta los componentes a los nativos (segmented controls, navigation bars)"

  - name: material_components
    target: ["app_android"]
    rule:
      - inconsistent_use_of_Material3_tokens (radius, elevation, color_roles) -> issue
    output_template:
      platform: "android"
      problem: "Uso inconsistente de los componentes Material"
      recommendation_patterns:
        - "Usa los tokens de Material 3 (elevation, corner radius, color roles) de forma coherente"

# 3. Typography & spacing by platform

check:
  - name: platform_typography_scale
    target: ["app_ios","app_android"]
    rule:
      - not_using_platform_typography_scale -> warning
    output_template:
      problem: "Escala tipográfica no alineada con la plataforma"
      recommendation_patterns:
        - "Ajusta tamaños a la escala recomendada (SF / Roboto / tokens Material)"

# 4. Gestures & affordances

check:
  - name: back_navigation
    target: ["app_ios","app_android"]
    rule:
      - no_visible_back AND no_gesture_back -> issue
    output_template:
      problem: "Falta patrón de vuelta atrás claro"
      recommendation_patterns:
        - "Asegura botón de back en la barra de navegación o gesto consistente con la plataforma"

## platform_checklist
- ¿La navegación principal está alineada con los patrones de la plataforma?
- ¿Se usan componentes nativos o equivalentes coherentes?
- ¿La tipografía y el espaciado respetan escalas de la plataforma?
- ¿Los gestos básicos (back, scroll, swipe) son consistentes con las expectativas del SO?