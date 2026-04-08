# Don’t Make Me Think (Steve Krug) — Guía para IA

## 0. Rol de este archivo

Este documento define cómo la IA debe evaluar claridad, intuición y carga cognitiva de una interfaz, basándose en las ideas de Steve Krug.

---

## 1. Principios fundamentales

### 1.1 “No me hagas pensar”

- El usuario no debería tener que pararse a descifrar cómo usar la interfaz.
- Señales:
  - Preguntas mentales como “¿dónde hago clic?”, “¿qué significa esto?”.
  - Elementos ambiguos o jerarquías visuales confusas.
- Cómo debe pensar la IA:
  - Evaluar si el propósito de la pantalla se entiende en 3–5 segundos.
  - Ver si la acción principal es obvia a simple vista.

Ejemplo IA:  
> “El objetivo principal de esta pantalla no es evidente en un vistazo. Ajusta el título, subtítulo y CTA para dejar claro qué debe hacer el usuario.”

---

### 1.2 El usuario escanea, no lee

- Los usuarios leen en diagonal, buscando pistas visuales y palabras clave.
- Aplicaciones:
  - Encabezados, destacados, bullets, tamaño/contraste de texto.
- Cómo debe pensar la IA:
  - Comprobar que hay una jerarquía clara de texto (títulos, subtítulos, bullets).
  - Detectar bloques largos de texto sin escaneabilidad.

Ejemplo IA:  
> “Hay párrafos largos sin encabezados ni bullets. Divide el contenido en bloques con titulares claros para facilitar el escaneo.”

---

### 1.3 Satisficing (elegir la primera opción razonable)

- El usuario no optimiza, elige lo primero que parece servir.
- Aplicación:
  - Orden y prominencia de opciones.
- Cómo debe pensar la IA:
  - Revisar qué elementos llaman más la atención primero.
  - Validar que lo más visible corresponde con el camino recomendado.

Ejemplo IA:  
> “El elemento que más destaca visualmente lleva a una ruta secundaria, no al flujo principal. Asegura que el CTA principal sea el más prominente.”

---

### 1.4 Convenciones y consistencia

- Las convenciones reducen el esfuerzo mental.
- Aplicación:
  - Ubicación de navegación, etiquetas, estados de links, etc.
- Cómo debe pensar la IA:
  - Detectar ruptura de convenciones sin beneficio claro.
  - Marcar inconsistencias de estilo o comportamiento.

Ejemplo IA:  
> “Los links a veces aparecen subrayados y otras veces no, sin criterio claro. Unifica la convención visual para reducir dudas.”

---

### 1.5 El “happy path” debe ser obvio

- Siempre debe existir una ruta clara para conseguir el objetivo principal.
- Cómo debe pensar la IA:
  - Identificar el objetivo principal de la pantalla.
  - Ver si la secuencia de pasos está clara y visible.

Ejemplo IA:  
> “Para completar la acción principal, el usuario debe descubrir un botón poco visible dentro de un menú desplegable. Mueve el CTA a una posición más evidente.”

---

## 2. Checklist IA de análisis rápido

Para cada pantalla, la IA contesta sí/no:

1. ¿Puedo describir en 1 frase qué hace esta pantalla sin leer todo?
2. ¿Es evidente cuál es el siguiente paso?
3. ¿Hay elementos que parecen clicables y no lo son?
4. ¿Hay texto o elementos visuales que no aportan valor al objetivo?
5. ¿La ruta principal se ve sin necesidad de explorar menús ocultos?

Si hay varios “no”, la IA debe generar issues detallados con recomendaciones.

---

## 3. Recomendaciones generadas por la IA

Cada issue basado en Krug debe incluir:

- `principle`: “Don’t Make Me Think”.
- `friction`: breve descripción de la duda que puede tener el usuario.
- `change`: acción de diseño clara (ej: “renombrar botón”, “aumentar contraste del CTA”, “reorganizar jerarquía visual”).

Ejemplo:

```json
{
  "principle": "DontMakeMeThink",
  "location": "Página de registro",
  "friction": "El usuario no sabe si está creando cuenta o iniciando sesión.",
  "change": "Separa ‘Crear cuenta’ y ‘Iniciar sesión’ en dos pestañas claramente etiquetadas."
}
```