# Strategic Writing for UX (Torrey Podmajersky) — Guía para IA

## 0. Rol de este archivo

Este documento define cómo la IA debe evaluar y mejorar el texto de la interfaz (microcopy, títulos, mensajes de error, vacíos de contenido).

---

## 1. Ejes de evaluación del copy

La IA evalúa cada fragmento de texto según cuatro ejes:

1. Propósito  
2. Conciso  
3. Conversacional  
4. Claro y orientado a la acción

---

## 2. Propósito

- Cada texto debe servir a una tarea específica del usuario o del negocio.
- Preguntas para la IA:
  - ¿Qué quiere lograr el usuario cuando lee esto?
  - ¿Está claro qué valor aporta este texto?
- Señales de problema:
  - Texto decorativo sin utilidad.
  - Mensajes que informan pero no guían.

Ejemplo IA:  
> “Este párrafo describe la funcionalidad, pero no explica qué gana el usuario. Añade una frase que conecte con el beneficio concreto.”

---

## 3. Conciso

- Menos palabras, mismo significado.
- Reglas:
  - Evitar redundancias y frases largas.
  - Eliminar palabras de relleno (“muy”, “bastante”, “en realidad”).
- Cómo debe actuar la IA:
  - Sugerir versiones más cortas manteniendo intención.
  - Resaltar frases que puedan reducirse.

Ejemplo IA:  
> Texto original: “En este momento nos encontramos procesando tu solicitud.”  
> Sugerencia IA: “Estamos procesando tu solicitud.”

---

## 4. Conversacional

- Hablar como una persona, no como un sistema.
- Características:
  - Segunda persona (“tú”, “tu cuenta”).
  - Sin jerga técnica innecesaria.
- Cómo debe actuar la IA:
  - Detectar tecnicismos y proponer alternativas claras.
  - Ajustar tono a contexto (más formal en banca, más cercano en apps sociales).

Ejemplo IA:  
> “Reemplaza ‘instanciar recurso’ por ‘crear recurso’ para que cualquier usuario lo entienda.”

---

## 5. Claro y orientado a la acción

- Especialmente importante en botones y mensajes de sistema.
- Botones:
  - Usar verbos + objeto: “Guardar cambios”, “Crear cuenta”, “Descargar informe”.
  - Evitar: “OK”, “Hecho”, “Aquí”, “Continuar” sin contexto.
- Mensajes de error:
  - Qué pasó + qué hacer ahora.
- Estados vacíos:
  - Explicar qué falta y cómo empezar.

Ejemplos IA:  
> “Reemplaza ‘Click aquí’ por ‘Guardar cambios’ para clarificar la acción.”  
> “Este error solo dice ‘Ha ocurrido un problema’. Añade una instrucción: ‘Intenta subir un archivo en formato PDF o JPG’.”

---

## 6. Checklist IA para tipos de texto

### 6.1 Botones

- ¿Describe claramente la acción?
- ¿Empieza con un verbo?
- ¿Hay dos botones con copy demasiado similar?

### 6.2 Mensajes de error

- ¿Indican qué pasó?
- ¿Indican al menos un siguiente paso?

### 6.3 Títulos y subtítulos

- ¿Responden a “¿qué puedo hacer aquí?”?
- ¿Son escaneables y directos?

### 6.4 Onboarding y vacíos de contenido

- ¿Explican beneficio antes de pedir esfuerzo?
- ¿Incluyen una llamada a la acción concreta?

---

## 7. Formato de salida sugerido

```json
{
  "component": "primary_button",
  "text_original": "OK",
  "issues": ["no_action_oriented", "too_generic"],
  "suggestion": "Guardar cambios",
  "rationale": "El texto debe describir la acción concreta según las pautas de microcopy."
}
```