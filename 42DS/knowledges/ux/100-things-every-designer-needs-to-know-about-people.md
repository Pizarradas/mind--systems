# 100 Things Every Designer Needs to Know About People (Susan Weinschenk) — Guía para IA

## 0. Rol de este archivo

Este documento traduce insights de psicología en heurísticas para que la IA evalúe percepción, memoria, atención y motivación de los usuarios.

---

## 1. Percepción y atención

### 1.1 La gente ve primero el conjunto, luego los detalles

- La primera impresión es global: layout, bloques, pesos visuales.
- Acción IA:
  - Evaluar si la estructura general se entiende en un vistazo.
  - Ver si el diseño tiene un foco visual claro.

Ejemplo IA:  
> “La pantalla no tiene un punto focal claro; varios elementos compiten por la atención al mismo nivel. Ajusta la jerarquía visual.”

---

### 1.2 La atención es limitada

- Muchos estímulos compiten entre sí.
- Acción IA:
  - Detectar elementos que distraen de la tarea principal (banners, animaciones, mensajes secundarios).
  - Recomendar reducción o reubicación.

Ejemplo IA:  
> “Hay múltiples banners animados cerca del formulario principal. Redúcelos o muévelos para proteger la atención del usuario.”

---

## 2. Memoria y carga cognitiva

### 2.1 Memoria de trabajo limitada

- Las personas solo pueden retener unos pocos ítems a la vez.
- Acción IA:
  - Detectar pasos que exigen recordar datos de pantallas anteriores.
  - Sugerir resúmenes, migas de pan, vistas de comparación.

Ejemplo IA:  
> “El usuario debe recordar 3 códigos a la vez para completar el proceso. Añade un resumen visible con los códigos seleccionados.”

---

### 2.2 Reconocimiento mejor que recuerdo

- Es más fácil reconocer opciones que recordar datos.
- Acción IA:
  - Priorizar listas y sugerencias sobre campos vacíos que obligan a recordar.
  - Sugerir auto-completado, historial, selecciones recientes.

Ejemplo IA:  
> “En lugar de exigir que el usuario recuerde el ID del proyecto, ofrece una lista desplegable con nombres y búsqueda.”

---

## 3. Motivación y emoción

### 3.1 La gente responde a beneficios claros

- “¿Qué gano yo haciendo esto?”
- Acción IA:
  - Detectar textos que piden esfuerzo sin explicar beneficios.
  - Proponer añadir frases de resultado (“Obtendrás X”, “Esto te permite Y”).

Ejemplo IA:  
> “Esta pantalla pide verificar el correo sin explicar por qué. Añade un beneficio: ‘Así protegemos tu cuenta y tus datos’.”

---

### 3.2 Feedback inmediato refuerza la acción

- Sin feedback, el usuario siente pérdida de control.
- Acción IA:
  - Verificar loaders, toasts y confirmaciones rápidas.
  - Marcar acciones silenciosas.

Ejemplo IA:  
> “Después de enviar el formulario, no se muestra ninguna confirmación. Añade un mensaje de éxito claro.”

---

### 3.3 Pequeñas recompensas y progreso visible

- Ver progreso mantiene la motivación.
- Acción IA:
  - Recomendar barras de progreso en flujos largos.
  - Sugerir logros o micro-recompensas donde tenga sentido.

Ejemplo IA:  
> “El flujo de registro tiene 4 pasos pero no muestra progreso. Añade un indicador de pasos (1/4, 2/4, etc.) para reducir la incertidumbre.”

---

## 4. Checklist IA

1. ¿Hay demasiados elementos compitiendo por atención?
2. ¿La pantalla comunica de un vistazo qué es importante?
3. ¿Se está obligando al usuario a recordar información que podría verse?
4. ¿Se explica el beneficio de acciones costosas?
5. ¿Hay feedback inmediato en acciones clave?
6. ¿Se muestra progreso en flujos de varios pasos?

---

## 5. Formato de salida sugerido

```json
{
  "dimension": "attention_memory_motivation",
  "location": "Flujo de registro paso 3",
  "issue": "no se muestra progreso y el usuario debe recordar información previa",
  "severity": "medium",
  "recommendation": "Añade una barra de progreso y un resumen de la información ya completada para reducir la carga cognitiva y aumentar la motivación."
}
```