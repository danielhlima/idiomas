# Lección 9 — Completion checkpoint

## Objective and scope
Complete `Gran repaso de vacaciones` in `Leccion09/`: add Slides 60–89, a 20-item adverb workbook, three original readings with comprehension activities, seven guided writing slides, final review/study guidance, and a nine-block Cuaderno with exactly 120 items. No deploy. Preserve Lecciones 1–8 and existing Lección 9 content except minimal deck-runtime integration required by new slides.

## Permanent rules
- Visible student content in Spanish; use only grammar and vocabulary taught in Lecciones 1–8.
- No listening/audio, generated/external images, outside AI APIs, past tenses, subjunctive, future simple, or conditional.
- Follow English-course slide system + Spanish palette; preserve 16:9 runtime, navigation, progress, toolbar, keyboard, accessibility, responsive behavior.
- Progressive reveals need Spanish live step counters; answers/models stay hidden until requested.
- Workbooks use `WORKBOOK_STANDARD.md`: one item per step, correct answers required to advance, every submitted attempt counted once, errors retained, canonical precision `completed / attempts`, one final `REPETIR EJERCICIO` button, unique best-result localStorage key. No answer/session persistence exists in current workbook examples; don't promise resume.
- Open productions receive structural checks/review guidance only, never a claim of full linguistic correction.

## Baseline inspection
- `Leccion09/index.html` contains 55 actual slide sections with sparse IDs ending at `slide-59`; Slides 58 and 59 are present.
- Existing Leccion09 workbooks: 09-01, 09-02, 09-03, 09-04.
- Runtime is local to the lesson and computes slide count from DOM sections.
- Existing canonical docs have pre-existing working-tree modifications; preserve them.
- Browser preview of local `file://` pages is unavailable in this environment; use static/automated validation and report the limitation.

## Planned slide map
- 60–66: adverbs (`-mente`; coordinated adverbs; quantity/manner; time; place; direction; `con/sin`).
- 67: launcher for 20-item adverb workbook.
- 68–73: three original readings (routine, two families, complicated day) and comprehension.
- 74–80: seven guided production slides with optional models.
- 81–86: exact diagnostic return, grammar/vocabulary maps, common errors, self-assessment, flexible holiday study plan.
- 87–89: Cuaderno overview, operating guidance, final launcher.

## Workbook distribution
- Adverb workbook: exactly 20 items; target 16 typed and 4 choice, including at least four full-sentence/writing items.
- Cuaderno: 120 items in 9 blocks: 14, 14, 14, 14, 10, 12, 18, 14, 10 respectively; target at least 84 typed and all 10 final integrated-production items written.

## Progress
- [x] Read `AGENTS.md`, English and Spanish slide guides, `WORKBOOK_STANDARD.md`, and the full task specification.
- [x] Inspect Leccion09 slide inventory, current runtime, exercise inventory, and representative Slides 1–59.
- [x] Read-only delegated audits started: vocabulary/source audit and workbook architecture audit.
- [x] Record baseline and plan.
- [x] Complete source vocabulary audit for Lecciones 1–8 and confirm diagnostic Slide 4 copy.
- [x] Confirmed current deck has 55 actual slide sections with sparse IDs ending at 59; exact Slide 4 diagnostic prompts recorded.
- [x] Confirmed no progress/session persistence exists in existing workbooks beyond saving best precision.
- [x] Reviewed the pre-existing 09-04 custom “autonomous precision” formula. The task explicitly says to preserve previous exercises, so it was left unchanged; both new workbooks use canonical `completed / attempts`.
- [x] Implement/validate Slides 60–67 and adverb workbook.
- [x] Implement/validate Slides 68–73 and three readings/comprehension.
- [x] Implement/validate Slides 74–80.
- [x] Implement/validate Slides 81–86.
- [x] Implement/validate Slides 87–89 and 120-item Cuaderno.
- [x] Integrated QA, update file list/results, final report.

## Files created/changed in this task
- Created: `Curso de Espanhol/docs/leccion-9-completion.md`.
- Pending implementation: `Curso de Espanhol/Leccion09/index.html`; `workbook/leccion-09/` new exercise files.

## Source audit highlights
- Verified L8 adverb inventory includes -mente forms, coordinated adverbs, quantity/mode/time/place/direction, and `con/sin` phrases; preserve nuance for `aquí/acá`, `allí/allá`, adverb function, and approximate `con/sin` equivalents.
- `El tren` and `La cita` are valid source contexts; avoid their advanced grammar and keep new readings in present indicative / taught `ir a + infinitivo`.
- Slide 4 diagnostic questions/answers: hay; trabaja; estudiar; su; aquel; más / bien. Reuse exactly on Slide 81.
- Current lesson checkout/readings/workbook patterns were audited read-only.

## Next step
Implement and validate the adverb block (Slides 60–67) while independent agents prepare the three reading draft and Cuaderno workbook file.

## Implementation completed
- [x] Slides 60–67: seven progressive adverb lessons with live Spanish stage counters, answer reveals, and the standalone exercise launcher.
- [x] Adverb workbook: exactly 20 items (12 typed short responses, 4 selected responses, 4 open written responses); accepts each item only after submission and records every submitted attempt.
- [x] Slides 68–73: three original readings and 10/12/12 comprehension prompts with answer reveal; reading bodies contain 178, 275, and 343 whitespace-separated words respectively.
- [x] Slides 74–80: seven guided writing prompts with checklists and optional sample models; no automated language grades.
- [x] Slides 81–86: exact Slide 4 diagnostic questions, grammar and vocabulary maps, 18 frequent-error examples in short progressive groups, communicative self-assessment, and flexible 12-session study suggestion.
- [x] Slides 87–89: workbook overview, truthful operation and persistence notes, final launcher.
- [x] Cuaderno: 120 items distributed 14/14/14/14/10/12/18/14/10; 88 typed-response items, 17 choice items, 15 open responses, with all 10 final items in the integrated-production block.

## Files added or changed for this work
- `Leccion09/index.html` — appended Slides 60–89 and added namespaced styling, reveal handling, and progressive navigation integration.
- `Leccion09/workbook/leccion-09/ejercicio-09-05-adverbios-y-expresiones.html` — new 20-item standalone adverb exercise.
- `Leccion09/workbook/leccion-09/cuaderno-de-vacaciones.html` — new 120-item standalone workbook.

## Validation performed
- Node syntax-compiled inline JavaScript from the deck and both new workbooks.
- Confirmed 85 total actual slide sections after adding 30 new slides, with IDs `slide-60` through `slide-89`; every new slide has the expected section label, `tabindex="-1"`, hidden initial state, and slide progress/count footer.
- Checked duplicate IDs and `aria-controls` references in the new slides and workbooks; no duplicate IDs or missing targets in new material.
- Confirmed reading lengths, exercise totals, required nine-block distribution, 20-item adverb distribution, and the ten final open Cuaderno items.
- Confirmed both workbook launch links point to existing files.
- Local browser preview was unavailable because the computer-use browser rejected local `file://` navigation; no visual screenshot QA was performed. No deploy was done.

## Notes
- Workbooks retain only the best precision in local storage; answers and active session progress are not persisted. The final slide copy describes this accurately.
- Existing unrelated working-tree changes were present before this work and were left untouched.

- Pre-existing exercise 09-04 continues to label its separate aided/unaided measure as “Precisión autónoma”; this differs from the canonical measure. It was not altered because the task expressly preserves prior exercises.
