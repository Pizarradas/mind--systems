# The Design of Everyday Things (Don Norman) — Guía para IA

## 0. Rol de este archivo

Este documento ayuda a la IA a evaluar la relación entre forma y función: qué se puede hacer y cómo se comunica esa posibilidad.

---

## 1. Conceptos clave

### 1.1 Affordance

- Acción posible con un objeto o elemento.
- En interfaces:
  - Se puede hacer clic, arrastrar, escribir, deslizar, etc.

### 1.2 Signifier

- Señales que indican que la acción es posible.
- Ejemplos:
  - Forma de botón, sombra, icono, cursor, placeholder, animación.

---

## 2. Cómo debe evaluar la IA affordances y signifiers

### 2.1 Controles que no parecen controles

- Problema:
  - Elementos interactivos que parecen texto estático o decoración.
- Acción IA:
  - Detectar botones sin estilo de botón.
  - Recomendar añadir signifiers claros (color, borde, relieve, icono).

Ejemplo IA:  
> “El texto ‘Aplicar filtros’ es clicable, pero no tiene estilo de botón. Añade fondo o borde para indicar que es interactivo.”

---

### 2.2 Estados claros (hover, activo, deshabilitado)

- Estados deben ser distinguibles sin esfuerzo.
- Acción IA:
  - Revisar contraste y cambio visual entre estados.
  - Marcar estados deshabilitados apenas distinguibles.

Ejemplo IA:  
> “El estado deshabilitado solo tiene una ligera reducción de opacidad. Aumenta la diferencia para evitar que el usuario intente interactuar con él.”

---

### 2.3 Mapeo natural

- Relación intuitiva entre controles y resultados.
- Ejemplos:
  - Botones de avance a la derecha, retroceso a la izquierda.
  - Volumen ↑ cuando el slider se mueve hacia arriba/derecha.
- Acción IA:
  - Detectar inconsistencias (ej: flecha izquierda que avanza).
  - Sugerir mapeos estándar.

Ejemplo IA:  
> “El botón con flecha hacia la derecha lleva a la pantalla anterior. Intercambia la dirección o el comportamiento para que el mapeo sea lógico.”

---

### 2.4 Feedback

- El sistema debe responder de forma visible a las acciones.
- Tipos:
  - Cambios de estado, loaders, mensajes de confirmación.
- Acción IA:
  - Verificar que cada acción relevante produce feedback visible a tiempo.
  - Detectar operaciones sin señal de progreso.

Ejemplo IA:  
> “Tras pulsar ‘Guardar’, no se muestra feedback hasta varios segundos después. Añade un indicador de carga inmediato.”

---

## 3. Checklist IA

Para cada elemento interactivo, la IA debe responder:

1. ¿Es claramente reconocible que es interactivo?
2. ¿Su icono o forma comunica la acción correctamente?
3. ¿Sus estados (normal, hover, activo, deshabilitado) son distinguibles?
4. ¿La posición de los controles tiene un mapeo natural con el resultado?
5. ¿La acción genera feedback inmediato y comprensible?

---

## 4. Formato de salida sugerido

```json
{
  "concept": "affordance_signifier",
  "location": "Botón 'Eliminar cuenta'",
  "issue": "parece enlace de texto en vez de botón de acción crítica",
  "severity": "high",
  "recommendation": "Usa un botón con color y icono de advertencia para resaltar la naturaleza de la acción."
}
```