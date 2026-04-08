# Laws of UX (Jon Yablonski) — Guía para IA

## 0. Rol de este archivo

Este documento sirve como marco de evaluación basado en psicología y usabilidad.  
Objetivo: que la IA pueda detectar violaciones de leyes de UX, explicar el problema y proponer cambios concretos.

---

## 1. Principios clave que debe conocer la IA

### 1.1 Ley de Hick

- Cuantas más opciones simultáneas, más tiempo tarda el usuario en decidir.
- Aplicaciones principales:
  - Menús de navegación, listas de opciones, configuraciones, filtros.
- Reglas prácticas:
  - Menú principal: idealmente 5–7 opciones visibles.
  - Listas de acciones: agrupar cuando haya más de 7 elementos.
- Cómo debe pensar la IA:
  - Detectar pantallas con demasiadas opciones visibles a la vez.
  - Proponer agrupación, progresión por pasos o filtros progresivos.

Ejemplo de mensaje IA:  
> “Este menú muestra 12 opciones principales. Según la Ley de Hick, esto incrementa el tiempo de decisión. Agrupa en categorías y reduce las opciones visibles a 5–7.”

---

### 1.2 Ley de Fitts

- El tiempo para alcanzar un objetivo depende de su tamaño y distancia.
- Aplicaciones:
  - Botones, enlaces, controles interactivos (sobre todo en mobile).
- Reglas prácticas:
  - Tamaño mínimo recomendado de objetivos táctiles: ~44×44 px.
  - Mayor tamaño para acciones críticas (ej: CTA principal).
  - Distancia pequeña entre control y elemento al que afecta.
- Cómo debe pensar la IA:
  - Detectar objetivos pequeños o muy próximos a bordes difíciles.
  - Detectar botones principales demasiado alejados del contenido relevante.

Ejemplo IA:  
> “Los botones de acción principal son pequeños y están alejados del contenido que modifican. Aumenta el tamaño del área clicable y acércalos al elemento relacionado.”

---

### 1.3 Ley de Miller / Chunking

- Las personas pueden manejar un número limitado de ítems a la vez (≈ 7 ± 2).
- Aplicaciones:
  - Menús, formularios largos, listados extensos, pasos de un flujo.
- Reglas prácticas:
  - Agrupar campos de formulario en secciones pequeñas (4–7 campos).
  - Dividir procesos largos en pasos (wizard).
- Cómo debe pensar la IA:
  - Detectar pantallas que exigen procesar demasiados elementos sin agrupación.
  - Recomendar grupos con títulos claros o pasos secuenciales.

Ejemplo IA:  
> “Este formulario muestra 18 campos en un solo bloque. Divide el formulario en secciones temáticas de 5–7 campos para reducir la carga cognitiva (Ley de Miller).”

---

### 1.4 Efecto de Usabilidad Estética

- Los usuarios perciben los diseños atractivos como más usables, incluso si hay pequeños problemas.
- Aplicaciones:
  - Diseño visual, consistencia, alineaciones, espacios, tipografía.
- Cómo debe pensar la IA:
  - Valorar coherencia visual y estética general.
  - Advertir cuando un diseño “bonito” oculta fricciones graves.

Ejemplo IA:  
> “La interfaz es visualmente atractiva y consistente, lo que mejora la percepción de usabilidad. Sin embargo, la complejidad del menú sigue siendo alta; no confíes solo en la estética.”

---

### 1.5 Ley de Jakob

- Los usuarios esperan que tu producto funcione como otros que ya conocen.
- Aplicaciones:
  - Posición de navegación, iconos estándar, patrones comunes.
- Cómo debe pensar la IA:
  - Detectar desviaciones fuertes de patrones consolidados (logo, carrito, iconos comunes).
  - Diferenciar entre innovación útil y ruptura innecesaria.

Ejemplo IA:  
> “El icono de menú está en un lugar poco habitual y el patrón difiere de la mayoría de aplicaciones similares. Esto viola las expectativas previas del usuario (Ley de Jakob). Considera usar una posición más convencional.”

---

## 2. Checklist para la IA

Para cada pantalla, la IA debe:

1. Contar cuántas opciones principales se muestran (Ley de Hick, Miller).
2. Revisar tamaño y distancia de objetivos clave (Ley de Fitts).
3. Evaluar si hay agrupación lógica de elementos (Chunking).
4. Comprobar coherencia visual y orden (Efecto de Usabilidad Estética).
5. Validar si patrones básicos coinciden con apps/webs estándar (Ley de Jakob).

---

## 3. Formato de salida sugerido

Cada hallazgo relacionado con Laws of UX debe incluir:

- `law`: nombre de la ley.
- `location`: lugar en la interfaz.
- `description`: qué problema se observa.
- `impact`: alto / medio / bajo.
- `recommendation`: cambio específico.

Ejemplo:

```json
{
  "law": "Hick + Miller",
  "location": "Menú lateral",
  "description": "Se muestran 15 opciones al mismo nivel.",
  "impact": "high",
  "recommendation": "Agrupa las opciones en 3–4 categorías y limita a 6–7 ítems visibles."
}
```