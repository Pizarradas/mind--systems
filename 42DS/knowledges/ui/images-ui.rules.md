# Images & Photography in UI — Reglas para IA

## meta
- domain: ui
- subdomain: images
- sources:
  - Best practices de uso de fotografía en UI (Eagle, blogs de producto)
- goal: evaluar uso de fotografías e imágenes raster en la interfaz

## dimensions_enabled
- relevance
- style_and_brand
- text_on_image
- performance

# 1. Relevancia (relevance)

check:
  - name: image_supports_content
    target: ["image"]
    rule:
      - context in ["hero","card","promo"] AND image_unrelated_to_text -> warning
    output_template:
      dimension: "relevance"
      problem: "Imagen poco relacionada con el contenido"
      recommendation_patterns:
        - "Usa imágenes que refuercen el mensaje o muestren el producto real"

# 2. Estilo y marca (style_and_brand)

check:
  - name: image_style_consistency
    target: ["image_set"]
    rule:
      - mixed_color_grading OR mixed_aspect_ratios_without_pattern -> warning
    output_template:
      dimension: "style_and_brand"
      problem: "Fotografías con estilos muy diferentes"
      recommendation_patterns:
        - "Unifica proporciones, tratamiento de color y encuadre según la marca"

  - name: over_stock_feel
    target: ["hero_image"]
    rule:
      - stock_cliche_score_high -> warning
    output_template:
      dimension: "style_and_brand"
      problem: "Imagen de stock genérica que no aporta identidad"
      recommendation_patterns:
        - "Prioriza imágenes propias o stock más específico de tu producto/usuarios"

# 3. Texto sobre imagen (text_on_image)

check:
  - name: text_contrast_on_image
    target: ["text_over_image"]
    rule:
      - contrast_ratio(text,local_background) < 4.5 -> issue
    output_template:
      dimension: "text_on_image"
      problem: "Contraste insuficiente del texto sobre la imagen"
      recommendation_patterns:
        - "Añade overlay, blur o caja sólida hasta lograr contraste adecuado"

  - name: busy_background
    target: ["text_over_image"]
    rule:
      - background_detail_level_high -> warning
    output_template:
      dimension: "text_on_image"
      problem: "Fondo demasiado ‘ruidoso’ detrás del texto"
      recommendation_patterns:
        - "Simplifica el fondo (blur, recorte) o mueve el texto a zona limpia"

# 4. Performance (tamaño y formato)

check:
  - name: image_size_reasonable
    target: ["image"]
    rule:
      - file_size_mb > threshold_for_context -> warning
    output_template:
      dimension: "performance"
      problem: "Imagen posiblemente demasiado pesada"
      recommendation_patterns:
        - "Optimiza formato (WebP/AVIF) y resolución según el uso"

  - name: responsive_crops
    target: ["hero_image","banner"]
    rule:
      - same_crop_desktop_mobile AND important_subject_cut_on_mobile -> issue
    output_template:
      dimension: "performance"
      problem: "Recorte no adaptado a mobile"
      recommendation_patterns:
        - "Define crops específicos por breakpoint para preservar el sujeto principal"