# Guía de desarrollo de slides — Curso de Español

## Regla principal

**Identidad visual española + mecánicas arquitectónicas del Curso de Inglés.**

Las Lecciones 1–4 son referencias visuales y pedagógicas ya funcionales. No se migran ni se refactorizan salvo petición explícita. Estas reglas se aplican desde la **Lección 5**.

## Dónde crear una lección nueva

Cada lección nueva es autocontenida:

```text
Curso de Espanhol/
  LeccionNN/
    index.html
    assets/
      images/
      audio/
      videos/
    workbook/
```

- La presentación vive en `LeccionNN/index.html`.
- Los assets pertenecen a la carpeta de la lección; no usar assets de otra lección sin petición explícita.
- Los ejercicios y la tarea son HTML independientes dentro de `LeccionNN/workbook/`.
- No modificar archivos de Lecciones 1–4 para integrar una lección nueva.

## Identidad visual: fuente de verdad española

Conservar la estética editorial adulta de las Lecciones 1–4: tipografía `Inter, Segoe UI, Arial, sans-serif`, fondos claros cálidos, cards blancos redondeados, sombras discretas, títulos oscuros, acento rojo y detalles dorados.

Usar los valores existentes, no crear otra paleta:

```css
--red: #aa151b;
--gold: #f1bf00;
--ink: #172033;
--muted: #667085;
--paper: #fffdf8;
--blue: #2d5ea8;
--green: #2d7a5b;
--soft: #f4efe4;
--focus: rgba(45, 94, 168, .38);
--line: rgba(23, 32, 51, .11);
```

Mantener la lógica de fondo actual (gradiente claro con halo dorado sutil), bordes suaves, progreso rojo→dorado y botones con el lenguaje visual existente. Reutilizar los tokens de espaciado, radio, fuente y escala de la lección antes de añadir CSS.

## Barra de navegación superior obligatoria

Cada lección nueva debe tener una barra fija en la parte superior, visible sobre todos los slides. Reutilizar el patrón `deck-toolbar` / `slide-nav`: botones **Anterior** y **Siguiente**, selector del slide actual y controles A− / A / A+.

```html
<nav class="deck-toolbar" aria-label="Controles de la lección" data-no-slide-advance>
  <div class="slide-nav" aria-label="Navegación de slides">
    <button type="button" data-slide-prev aria-controls="lesson-deck">Anterior</button>
    <button type="button" data-slide-next aria-controls="lesson-deck">Siguiente</button>
  </div>
  <select data-slide-select aria-label="Ir a un slide"></select>
  <button type="button" data-font-size="small" aria-label="Reducir texto">A−</button>
  <button type="button" data-font-size="normal" aria-label="Restaurar texto">A</button>
  <button type="button" data-font-size="large" aria-label="Aumentar texto">A+</button>
</nav>
```

El runtime llena el selector como `1. Título del slide`, sincroniza su valor, y desactiva **Anterior** en el primer slide y **Siguiente** en el último. La barra debe mantener el estilo visual español y espacio suficiente en el encabezado para no cubrir contenido, también en móvil.

## Forma estándar de slide

Usar el deck semántico y de viewport completo del Curso de Inglés. La primera slide es la única activa al cargar, salvo que el hash indique otra.

```html
<section class="slide repaso-ser-estar-slide" id="slide-repaso-ser-estar"
  data-slide aria-labelledby="slide-repaso-ser-estar-title" tabindex="-1" hidden>
  <header class="slide-header">
    <p class="slide-kicker">Lección N · Repaso</p>
    <h2 id="slide-repaso-ser-estar-title">Título del slide</h2>
    <p class="slide-subtitle">Instrucción breve en español.</p>
  </header>

  <div class="slide-content">
    <!-- contenido solicitado -->
  </div>

  <footer class="slide-footer">
    <div class="slide-progress" data-slide-progress role="progressbar"
      aria-label="Progreso de la lección"><span></span></div>
    <p class="slide-count" data-slide-count>Slide N / N</p>
  </footer>
</section>
```

Mantener `.course-app`, `.lesson-deck`, `.slide`, `.slide-header`, `.slide-content`, `.slide-footer`, `.slide-progress` y `.slide-count`. El runtime calcula el total, contador, `aria-valuemax`, `aria-valuenow` y ancho del progreso desde el DOM: no mantener esos números a mano.

## Runtime y navegación

- La lección conserva runtime local y autocontenido: estado del slide, hash, progreso, contador, foco, teclado, clic/touch, fullscreen, barra superior Prev/Next/select y controles A− / A / A+.
- Reutilizar helpers del `index.html` antes de escribir lógica nueva. Navegación: flechas, Page Up/Down, Space, Home/End y `F` para fullscreen cuando no se está escribiendo ni operando un control.
- El clic de fondo puede navegar; controles interactivos no. Proteger `a`, `button`, `input`, `label`, `select`, `textarea`, `audio`, `video`, `dialog`, contenido editable y `[data-no-slide-advance]`.
- En botones y controles internos, cancelar la propagación y, cuando corresponda, el teclado que podría avanzar el deck.
- Usar `hidden`, clase/estado activo y foco programático de forma coherente; no ocultar contenido solo visualmente si debe quedar fuera de la navegación por teclado.

## Patrones reutilizables

### Revelación progresiva

Mantener todas las etapas dentro de un slide real. Reutilizar `data-progressive-reveal`, `data-progressive-navigation`, `data-progressive-stage`, `data-progressive-counter`, `data-progressive-next` y `data-progressive-reset`.

- Las etapas no aumentan la cantidad de slides.
- El avance del deck revela primero la siguiente etapa; después de la última, avanza al siguiente slide.
- El botón interno y el reset no navegan el deck; el reset vuelve al estado inicial y actualiza contador/ARIA.
- Mantener el foco y el scroll interno previsible; no reducir la fuente para encajar muchas etapas.

### Quick check y práctica con corrección

- Usar una pregunta clara, control accesible, acción de comprobar o mostrar respuesta y feedback con `aria-live`.
- Para respuestas comprobables, declarar la solución en `data-answer` (o atributo namespaced equivalente si hay múltiples respuestas válidas).
- Marcar estados `is-correct` / `is-incorrect`, usar `aria-invalid` cuando aplique y limpiar feedback al editar o cambiar la respuesta.
- No entregar la respuesta en placeholders, hints o texto visible antes de comprobar.
- La lógica de cada actividad se inicializa una vez; no duplicar comprobadores si ya existe un helper compatible.
- Cuando una respuesta escrita sea incorrecta, el campo o control de respuesta debe quedar visualmente destacado en rojo (borde, fondo o texto), además del feedback textual. Las respuestas correctas pueden destacarse en verde.

#### Horas en respuestas

- Cuando una respuesta incluya una hora, aceptar cualquier forma gramaticalmente correcta y equivalente, salvo que el enunciado pida explícitamente una convención determinada.
- Incluir en `acceptedAnswers` las variantes naturales que correspondan al contexto, por ejemplo: `a la una`, `a las trece`, `a las 13:00`, `13:00`, `a la 1:00 pm` y `a la 1:00pm`.
- La respuesta-modelo puede mantener la forma preferida por el curso, pero no debe penalizar una equivalencia correcta de formato o de expresión horaria.
- Aplicar esta flexibilidad únicamente a la hora; el resto de la frase continúa evaluándose según la consigna (sujeto, verbo, negación, concordancia y demás elementos solicitados).

#### Variantes gramaticales en preguntas

- Antes de publicar una lista, hacer una revisión específica de cada ejercicio de pregunta: comprobar todas las formulaciones que mantengan el mismo verbo, significado e información solicitada. Registrar en `acceptedAnswers` las variantes válidas desde el inicio, incluyendo preguntas con `cuándo` / `a qué hora` cuando el contexto las permita, pronombres explícitos u omitidos y el sujeto antes o después del verbo.
- No considerar válida una variante que cambie el verbo, el tiempo, el contenido o la información que se pide. La flexibilidad gramatical debe conservar el sentido de la frase-base; no debe convertirse en una respuesta para otro ejercicio.
- Al crear una lista nueva, revisar y registrar desde el principio las variantes gramaticales, naturales y equivalentes que los alumnos puedan producir; no esperar a añadirlas ejercicio por ejercicio después de una prueba.
- Aceptar toda formulación gramaticalmente correcta que busque la información destacada, aunque no coincida con el orden o la redacción del modelo.
- En preguntas directas, no rechazar automáticamente variantes con el sujeto antes o después del verbo: `¿Dónde trabaja Marta?` y `¿Dónde Marta trabaja?` pueden corresponder a registros, variedades o focos distintos; mantener la primera como modelo neutro cuando convenga.
- Aceptar también pronombres explícitos y órdenes naturales, como `¿Con quién trabajas?`, `¿Con quién trabajas tú?` y `¿Con quién trabajo?`, siempre que el significado y el contexto sean compatibles.
- No penalizar una variante por ser menos frecuente si sigue siendo gramatical y busca exactamente la información solicitada. Si una respuesta es realmente incorrecta, marcar el campo o control en rojo y mostrar el modelo correcto.
- En ejercicios de conjugación que indiquen una persona, aceptar tanto la forma verbal sola (`trabajo`) como la forma con el pronombre explícito (`yo trabajo`), siempre que la concordancia sea correcta.

### Actividad A/B y modo profesor

Una actividad A/B debe incluir número de pareja, elección Alumno A / Alumno B, información complementaria y separada, aviso **NO ENSEÑES TU PANTALLA**, y una misión donde ambos preguntan y responden.

- Seguir los flujos de `Leccion03/workbook/leccion-03/` y `Leccion04/workbook/leccion-04/`: selección de pareja/rol, cambio de selección, varios casos y vista responsive.
- El código de profesor es siempre **555**. Debe mostrar a la persona docente las vistas A, B y las respuestas necesarias, sin crear slides extras de gabarito.
- Preferir `<dialog>` accesible para selección, confirmación y respuestas docentes cuando encaje; usar fallback `open`/`hidden` si el entorno lo necesita. Restituir el foco al disparador al cerrar.

### Media, workbook y tarea

- Usar un asset final solo cuando exista y guardarlo en `assets/images`, `assets/audio` o `assets/videos` de la lección. Para voz, preferir MP3 mono compacto si mantiene claridad.
- Si la especificación exige media sin asset final, usar únicamente un placeholder explícito: `IMAGE PLACEHOLDER - propósito`, `AUDIO PLACEHOLDER - propósito` o `VIDEO PLACEHOLDER - propósito`.
- No añadir media decorativa ni placeholders innecesarios.
- Los launchers abren HTML del `workbook/` en una pestaña nueva con `target="_blank" rel="noopener"`; conservar la apariencia española de `exercise-call` / `activity-button` o su equivalente local.
- Para ejercicios formales, `docs/WORKBOOK_STANDARD.md` es obligatorio: interfaz en español, feedback, validación, respuestas sin pistas, responsive y pantalla final con solo **Repetir ejercicio**.

## Naming y JavaScript

- Nombrar por slide/actividad: `slide-agenda-imposible`, `agenda-imposible-grid`, `data-agenda-check`, `createAgendaCheck(root)`.
- Evitar IDs, clases, atributos y funciones genéricos que puedan colisionar.
- Encapsular la lógica específica en una IIFE; exponer, como máximo, un initializer namespaced y llamarlo desde el boot de la lección después de crear los helpers globales locales.
- No añadir globals ad hoc a `window`, no repetir listeners ni implementar una segunda versión de una mecánica ya disponible.

## CSS, responsive y accesibilidad

- Conservar el viewport 16:9 y evitar scroll vertical de la página. Cuando haga falta, usar scroll interno controlado, reorganización responsive o reveal progresivo.
- Añadir CSS mínimo, scoped al slide/componente nuevo; evitar cambios globales y refactors preventivos.
- Comprobar desktop, notebook, tablet y móvil: sin texto cortado, overflow horizontal, cards fuera de pantalla, footer cubriendo contenido ni botones inaccesibles.
- Usar encabezados reales, `aria-labelledby`, labels, `aria-live`, `aria-expanded`, `aria-hidden`, `aria-invalid`, `:focus-visible` y diálogos accesibles solo cuando sean pertinentes.
- Todo texto visible va en español. Portugués solo si una traducción o contraste pedagógico lo solicita explícitamente.

## Minimal diff y validación

- Un pedido de “crear el Slide N” modifica únicamente ese slide y el CSS/JS mínimo para integrarlo.
- No reescribir slides previos, no renombrar APIs existentes ni extraer un runtime/CSS compartido sin una necesidad directa solicitada.
- Antes de entregar: comprobar sintaxis de scripts inline con Node cuando sea posible, cantidad de slides, progreso/contador, hash, controles pedidos, rutas de media, interacciones, accesibilidad básica y que no hubo cambios fuera del alcance.
