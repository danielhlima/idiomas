# Lección 4 — continuidad técnica

- Presentación principal: `../leccion_4_material_v01.html`.
- Referencia principal: `../leccion_3_material_v01.html`; conservar paleta, tipografía, espaciado, cards, footer, contador, progreso, controles de fuente, fullscreen, teclado, clic/touch y hash numérico.
- Slides: mantener `.slide > .top + .content + .foot`; el contador y el progreso se calculan desde el DOM con `refreshSlideMetadata()`, sin totales fijos.
- Revelación progresiva: reutilizar `data-progressive-reveal`, `data-progressive-navigation`, `data-progressive-stage`, `data-progressive-counter`, `data-progressive-next` y `data-progressive-reset`. Las etapas internas no cuentan como slides. La flecha izquierda vuelve al slide real anterior; al completar las etapas, el siguiente avance va al slide real siguiente.
- Actividades orales/A-B: crear HTML independiente en `../workbook/leccion-04/`, siguiendo `actividad-inventario.html`, `actividad-tres-ciudades.html`, `actividad-la-agenda.html` o `calentamiento-dos-apartamentos.html` de la Lección 3. Mantener pareja, Alumno A/B, information gap, “NO ENSEÑES TU PANTALLA”, participación de ambos y modo profesor con código `555` cuando aplique.
- Prácticas formales: crear `ejercicio-01-<slug>.html`, `ejercicio-02-<slug>.html`, etc. Seguir `WORKBOOK_STANDARD.md`; el resultado final debe ofrecer únicamente `Repetir ejercicio`.
- Links desde slides: `workbook/leccion-04/<archivo>.html`, siempre con `target="_blank" rel="noopener"`. Cards de prácticas usan `.exercise-call`; actividades orales usan `.activity-button`.
- Medios: guardar en `../assets/leccion-04/` y referenciar desde la presentación como `assets/leccion-04/<archivo>`.
- Al añadir, quitar o reordenar slides, conservar IDs accesibles, títulos asociados, `data-section`, footer y los inicializadores existentes. No modificar las Lecciones 1–3.
