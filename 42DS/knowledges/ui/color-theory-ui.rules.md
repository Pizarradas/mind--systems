# Color en UI (Erik D. Kennedy) — Reglas para IA

## meta
- domain: color-system
- source: "The Rules of Color" (Ensayos Learn UI Design)
- goal: evaluar y sugerir sistemas de color coherentes, legibles y estéticamente sólidos

## dimensions_enabled
- palette_structure
- hue_shifting
- contrast_wcag
- accent_usage

# 1. Palette structure

check:
  - name: neutral_and_accent_presence
    target: ["palette"]
    rule:
      - no_neutrals OR no_clear_accent -> issue
    output_template:
      dimension: "palette_structure"
      problem: "Paleta sin neutrales ni color de acento claro"
      recommendation_patterns:
        - "Define una escala de grises (neutrals) y 1–2 colores de acento principales"

  - name: shade_steps
    target: ["color_scale"]
    rule:
      - less_than_5_steps_per_color_family -> warning
    output_template:
      dimension: "palette_structure"
      problem: "Escala de color con pocos pasos"
      recommendation_patterns:
        - "Crea varias intensidades (p.ej. 50/100/200/400/700) por color clave"

# 2. Hue shifting (desplazamiento de tono)

check:
  - name: dirty_colors
    target: ["palette"]
    rule:
      - dark_shades_not_shifted AND light_shades_not_shifted -> warning
    output_template:
      dimension: "hue_shifting"
      problem: "Sombras/luces de color parecen “sucias” por no ajustar el tono"
      recommendation_patterns:
        - "Oscurecer colores moviendo el tono hacia azul/morado; aclararlos moviendo ligeramente hacia amarillo (según color base)"

# 3. Contrast WCAG

## Nota: usar fórmula WCAG:
## C = (L1 + 0.05) / (L2 + 0.05)
## donde L1 es la luminancia relativa más alta y L2 la más baja.
## La IA debe marcar texto con contraste < 4.5:1 (normal) y < 3:1 (grande).

check:
  - name: text_contrast
    target: ["text","icon"]
    rule:
      - role == "body_text" AND contrast_ratio(text,background) < 4.5 -> issue
      - role == "large_text_or_icon" AND contrast_ratio < 3.0 -> issue
    output_template:
      dimension: "contrast_wcag"
      problem: "Contraste de texto/ícono insuficiente (WCAG)"
      recommendation_patterns:
        - "Ajusta luminancia relativa del texto o fondo hasta alcanzar el ratio recomendado"

# 4. Accent usage (uso de acentos)

check:
  - name: overuse_of_accent_color
    target: ["screen"]
    rule:
      - accent_color_usage_ratio > threshold -> issue
    output_template:
      dimension: "accent_usage"
      problem: "Color de acento usado en exceso"
      recommendation_patterns:
        - "Reserva el color de acento para acciones principales y elementos clave"

  - name: insufficient_accent
    target: ["screen"]
    rule:
      - accent_color_absent AND need_for_focus == true -> warning
    output_template:
      dimension: "accent_usage"
      problem: "Falta de color de acento para guiar la atención"
      recommendation_patterns:
        - "Introduce un color de acento para CTA y estados importantes"

## palette_checklist
- ¿Existe una escala de grises usable (neutrals)?
- ¿Hay 1–2 colores de acento bien definidos?
- ¿Las variantes claras/oscuras del color usan hue shifting, no solo luminosidad?
- ¿Todo texto importante cumple contraste WCAG?
- ¿El color de acento guía la atención o está “por todas partes”?