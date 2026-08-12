# Workbook Interactivo — Estándar del Proyecto

## 1. Objetivo

Este documento define el estándar obligatorio para los ejercicios del Workbook Interactivo y su integración con las lecciones en slides.

Su objetivo es garantizar:

- consistencia visual;
- coherencia pedagógica;
- accesibilidad;
- mantenimiento sencillo;
- reutilización de componentes;
- navegación previsible;
- feedback claro;
- una experiencia uniforme para el alumno.

Todo nuevo ejercicio debe seguir este documento, salvo cuando una especificación indique explícitamente una excepción.

---

## 2. Regla de idioma

Todo el contenido visible del Workbook debe estar en español.

Esto incluye:

- títulos;
- subtítulos;
- instrucciones;
- preguntas;
- opciones;
- placeholders;
- botones;
- feedback;
- explicaciones;
- notas pedagógicas;
- mensajes de resultado;
- elementos visibles de navegación.

El portugués solo puede aparecer cuando el objetivo explícito del ejercicio sea traducir del portugués al español.

Nunca deben crearse ejercicios de traducción del español al portugués.

En ejercicios que no sean de traducción:

- no deben aparecer traducciones;
- no deben aparecer equivalentes en portugués;
- no debe utilizarse portugués como ayuda;
- no debe utilizarse portugués en feedback;
- no debe utilizarse portugués en placeholders.

Cuando un ejercicio incluya una frase de origen en portugués, ese contenido debe utilizar:

```html
lang="pt-BR"
```

---

## 3. Principios pedagógicos

Los ejercicios deben:

- reforzar el contenido presentado en la lección;
- trabajar una habilidad principal por pregunta;
- avanzar de reconocimiento a producción;
- evitar información innecesaria;
- exigir contexto suficiente para una única respuesta esperada;
- permitir que el alumno comprenda por qué una respuesta es correcta o incorrecta;
- aceptar respuestas válidas cuando la producción escrita admita variación natural.

Siempre que sea posible, los ejercicios deben evaluar:

- género;
- número;
- concordancia;
- selección adecuada;
- construcción de frases;
- uso contextual;
- producción escrita;
- integración de contenidos ya estudiados.

---

## 4. Diseño de preguntas

Cada pregunta debe ser didáctica, no solo gramaticalmente posible.

Antes de crear o alterar una pregunta, verificar:

- si el enunciado obliga a la respuesta esperada;
- si alguna opción alternativa también sería correcta sin contexto;
- si el bloque, la categoría o la descripción entregan la respuesta;
- si una pista, palabra base o ejemplo previo vuelve la respuesta demasiado obvia;
- si una respuesta natural del alumno debería ser aceptada.

Cuando una pregunta pueda tener más de una respuesta correcta:

- ajustar el contexto para que solo una respuesta sea adecuada; o
- aceptar todas las respuestas naturalmente válidas en `acceptedAnswers`; o
- convertir la pregunta a producción escrita si la selección múltiple se vuelve artificial.

Ejemplo de criterio: `¿______ estás?` debe indicar si se pregunta por estado o por ubicación. Sin contexto, `¿Cómo estás?` y `¿Dónde estás?` son posibles.

---

## 5. Tipos de actividad

Usar el tipo más adecuado para el objetivo:

- `choice`: selección única, con una sola respuesta correcta.
- `true-false`: verificación simple de una afirmación.
- `text`: producción escrita de una respuesta.
- `multi-text`: varios campos de respuesta relacionados.
- `matching`: relación entre elementos.
- `classification`: clasificación por categorías.
- `ordering`: ordenación de elementos.
- `select`: selección por campo cuando sea más claro que botones.

No usar selección única cuando dos opciones puedan ser correctas en el contexto presentado.

Cuando una pregunta de opción resulte débil o demasiado obvia, preferir producción escrita con un enunciado más guiado.

---

## 6. Estructura de datos

Cada pregunta debe utilizar una estructura coherente con el template actual.

Campos recomendados:

```js
{
  id: 1,
  block: "Nombre del bloque",
  category: "Nombre de la categoría",
  responseKind: "recognition | written | varied",
  type: "choice",
  format: "selection | completion | production | transformation",
  prompt: "Instrucción breve en español.",
  title: "Pregunta o frase principal.",
  options: ["Opción A", "Opción B", "Opción C", "Opción D"],
  acceptedAnswers: ["Respuesta correcta"],
  correctAnswer: "Respuesta correcta",
  correctText: "Texto modelo cuando aplique",
  explanation: "Explicación breve en español.",
  note: "Observación pedagógica que solo aparece después de responder."
}
```

Reglas:

- `id` no debe cambiar en ajustes puntuales.
- `block` no debe revelar la respuesta.
- `category` debe orientar el tema, no funcionar como pista.
- `acceptedAnswers` debe incluir variantes válidas esperables.
- `correctText` debe mostrar un modelo claro para producción escrita.
- `note` debe usarse solo para observaciones posteriores a la corrección.
- `baseWords` solo debe aparecer si realmente ayuda sin entregar la respuesta.

---

## 7. Alternativas y aleatorización

Las alternativas deben mantenerse aleatorizadas cuando el template lo permita.

Reglas:

- no remover `shuffle`;
- no fijar el orden de las opciones salvo instrucción explícita;
- mantener alternativas plausibles, pero incorrectas dentro del contexto;
- evitar opciones que sean correctas por interpretación alternativa;
- no usar opciones-trampa basadas en ambigüedad mal formulada.

En selección única, debe existir una sola respuesta adecuada al contexto.

---

## 8. Producción escrita

En preguntas de escritura:

- aceptar mayúsculas y minúsculas de forma flexible;
- considerar variantes con y sin puntuación final;
- incluir variantes naturales de artículo, pronombre o orden cuando sean correctas;
- no marcar como incorrecta una respuesta gramatical y contextualmente válida;
- explicar en feedback por qué una variante es posible cuando exista más de una forma aceptable.

Ejemplo: si se pide una frase con `vosotros`, `estar`, `en clase` y `por la mañana`, deben aceptarse variantes como `Vosotros estáis en clase por la mañana` y `Vosotros estáis en la clase por la mañana`.

---

## 9. Feedback

El feedback debe aparecer solo después de que el alumno responda.

Debe incluir:

- indicación de correcto o incorrecto;
- respuesta correcta o modelo esperado;
- explicación breve;
- nota pedagógica posterior cuando haya una distinción importante.

La nota pedagógica no debe aparecer:

- antes de responder;
- como pista;
- en el enunciado;
- en la categoría;
- en el bloque.

Cuando haya una respuesta posible en otro contexto, el feedback debe reconocerlo sin invalidar la corrección del ejercicio.

Ejemplo:

```js
explanation: "Usamos “cómo” para preguntar por el estado de una persona.",
note: "Sin el contexto, también sería posible preguntar “¿Dónde estás?” para saber la ubicación de una persona. Aquí preguntamos por su estado."
```

---

## 10. Resultado final

La pantalla final debe mostrar:

- puntuación obtenida;
- puntuación máxima;
- porcentaje;
- mensaje de desempeño;
- mejor resultado;
- resultado por competencia o bloque, cuando el ejercicio ya use esa estructura.

La pantalla final debe contener apenas un botón obligatorio:

**Repetir ejercicio**

Ese botón debe:

- reiniciar completamente el ejercicio;
- limpiar respuestas;
- limpiar intentos;
- reiniciar la barra de progreso;
- mantener solamente el mejor resultado guardado en `localStorage`.

No deben existir en la pantalla final:

- Volver a la Lección;
- Ejercicio anterior;
- Siguiente ejercicio;
- Volver al Workbook.

La navegación entre ejercicios pertenece al flujo normal del curso, no a la pantalla de resultado.

---

## 11. Puntuación y almacenamiento

Cada pregunta vale 1 punto, salvo especificación explícita.

Reglas:

- mantener la puntuación máxima coherente con el número real de preguntas;
- mantener el cálculo de porcentaje;
- mantener el mejor resultado guardado en `localStorage`;
- no alterar la clave de `localStorage` en ajustes puntuales;
- usar una clave única por lección y ejercicio para el mejor resultado;
- no modificar el resultado por competencia si el ajuste no exige eso.

Ejemplo de clave:

```js
const BEST_SCORE_KEY = "workbook-leccion-02-ejercicio-03-best-score";
```

---

## 12. Navegación e integración con la lección

Los links desde las lecciones hacia ejercicios deben abrir en una nueva pestaña del navegador.

Usar siempre:

```html
target="_blank" rel="noopener"
```

Los cards de ejercicio en slides deben usar el componente visual existente (`exercise-call`) y no deben cambiar la pestaña actual de la lección.

En slides finales de workbook o repaso, mostrar solo los links que la lección realmente debe destacar. Si la instrucción pide apenas el repaso general, remover los links de ejercicios anteriores y mantener solo el ejercicio de revisión general.

---

## 13. Estándar visual de los ejercicios

Los ejercicios deben seguir el estilo ya establecido:

- paleta del curso (`--red`, `--gold`, `--ink`, `--muted`, `--blue`, `--green`, `--soft`);
- fondo claro con gradiente suave;
- cabecera con `CURSO DE ESPAÑOL`;
- controles de fuente visibles;
- panel principal con progreso;
- estado de pregunta y puntuación;
- feedback en bloque propio;
- botones accesibles;
- layout responsivo sin overflow horizontal.

Cuando un card combine textos de jerarquías visuales distintas, como `b + small`, término + traducción, título + detalle o ejemplo + observación, los elementos no pueden quedar inline sin separación. El texto secundario debe aparecer como bloque (`display:block`) o dentro de un contenedor en columna (`display:flex; flex-direction:column`) con `gap` o `margin-top`. La separación mínima recomendada entre jerarquías es de `8px`, incluso con la fuente aumentada.

No rehacer la página entera cuando el pedido sea un ajuste puntual.

---

## 14. Estándar visual de las lecciones en slides

Las lecciones deben permanecer separadas en slides, siguiendo la arquitectura de la Lección 1.

Reglas para próximas lecciones:

- no convertir la lección en texto corrido;
- mantener navegación por slides;
- mantener el contador de slides actualizado;
- mantener botones A-, A+ y reset de fuente;
- permitir aumento de fuente hasta `FONT_MAX = 1.7`;
- mantener `FONT_STEP = 0.05`, lo que permite diez clics adicionales de A+ después del antiguo límite `1.2`;
- usar una clave de fuente por lección, como `leccion2FontScale`;
- la frase explicativa debajo de `CURSO DE ESPAÑOL` debe tener destacado visual equivalente al estándar actualizado;
- la línea explicativa debe quebrar bien en mobile y no causar overflow horizontal;
- textos de tamaños o pesos diferentes no deben tocarse visualmente; usar separación vertical clara entre título, subtítulo, traducción, explicación y ejemplos, con mínimo visual recomendado de `8px` cuando sean elementos consecutivos.

Cuando haya traducciones en slides, usarlas solo si son pedagógicamente necesarias. Conceptos gramaticales centrales pueden aparecer solo en español para no sobrecargar la lectura.

---

## 15. Organización de vocabulario

Cuando una lección compare español y portugués, organizar listas extensas en dos secciones:

- `Sustantivos iguales en español y portugués` o equivalente en español;
- `Otros sustantivos`, `Otros adjetivos` o equivalente en español.

Reglas:

- mantener el término español más grande y visible;
- mantener la traducción, cuando exista, en tamaño menor;
- separar visualmente el término principal y la traducción con bloque, `gap` o margen superior de al menos `8px`;
- no mezclar secciones si la comparación forma parte del objetivo;
- evitar listas visualmente densas sin separación clara.

---

## 16. Ajustes puntuales

Antes de alterar un ejercicio ya existente:

- inspeccionar el archivo actual;
- localizar exactamente la pregunta o bloque afectado;
- preservar arquitectura, puntuación, navegación, estilos y accesibilidad;
- alterar solo los datos relacionados con el problema;
- no modificar otras preguntas;
- no crear nuevos archivos;
- no remover `shuffle`;
- no alterar `localStorage`;
- no alterar resultado por competencia salvo instrucción explícita.

Después del ajuste:

- revisar el diff;
- confirmar que ninguna pregunta no solicitada cambió;
- validar que no hay errores de JavaScript;
- verificar que la puntuación sigue funcionando;
- verificar que el layout no presenta overflow horizontal en desktop y mobile.

---

## 17. Checklist de aceptación

Antes de entregar un nuevo ejercicio o ajuste:

- el contenido visible está en español;
- las preguntas no son ambiguas;
- las respuestas aceptadas incluyen variantes válidas;
- las opciones siguen aleatorizadas;
- el feedback explica la regla;
- las notas solo aparecen después de responder;
- la pantalla final tiene solo `Repetir ejercicio`;
- la clave de `localStorage` es correcta;
- los links desde la lección abren en una nueva pestaña;
- los controles A+ funcionan según el estándar;
- textos con fuentes distintas tienen espacio suficiente entre sí;
- no hay errores en consola;
- no hay overflow horizontal en desktop ni mobile.
