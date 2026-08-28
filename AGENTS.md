# Project Instructions

## Scope
- The English course lives in `english-course-template/`.
- Each lesson is a self-contained slide deck in `english-course-template/LessonNN/index.html`, with lesson assets under that lesson's `assets/` folder and homework under `workbook/`.
- Do not edit `Curso de Espanhol/` or unrelated lessons unless the user explicitly asks.

## Default Rule For New English Slides
When creating a new slide:

1. Inspect the relevant existing lesson and the closest reusable slide pattern first.
2. Reuse the established design system, slide structure, controls, and interaction patterns.
3. Implement only the requested slide content and requested unique behavior.
4. Do not modify unrelated slides, existing activities, existing answers, or lesson copy.
5. Do not refactor working code unless the requested slide genuinely requires it.
6. Make the smallest safe diff.
7. Preserve global presentation behavior: navigation, keyboard controls, font-size controls, progress, hash handling, focus behavior, accessibility, and responsive behavior.

## Presentation Conventions
- Preserve the full-viewport 16:9 classroom presentation feel. Slides must fit without vertical scrolling.
- Use the existing `.course-app`, `.lesson-deck`, `.slide`, `.slide-header`, `.slide-content`, `.slide-footer`, `.slide-progress`, and `.slide-count` conventions.
- Keep slide sections as `<section class="slide ...">` with `id`, `data-slide`, `aria-labelledby`, `tabindex="-1"`, and `hidden` unless active.
- The first slide is the only active slide on load unless a hash points to another slide.
- Let the existing JavaScript update slide counts and progress; static footer text can be approximate but should not break runtime updates.
- Use existing CSS tokens such as `--color-page`, `--color-surface`, `--color-surface-soft`, `--color-ink`, `--color-muted`, `--color-line`, `--color-accent`, `--color-accent-strong`, `--color-accent-soft`, `--color-warm`, `--color-warm-soft`, `--color-focus`, `--color-night`, spacing tokens, radius tokens, and `--slide-font-scale`.
- Preserve typography: body uses Arial/Helvetica style, display headings use Georgia/Times style, no negative letter spacing.

## Interaction Conventions
- Namespace slide-specific IDs, classes, data attributes, functions, and state with a semantic slide/activity prefix, for example `data-family-tree-check`, `family-tree-*`, `createFamilyTreeCheck`.
- Initialize slide-specific JavaScript from the lesson boot function after global deck helpers are created.
- Use `data-*` attributes for activity state and answers. Prefer structured arrays inside one namespaced function for item sets, prompts, answer reveal, and quick checks.
- For check-answer activities, follow existing patterns: `data-answer`, green correct state, red incorrect state, feedback via `aria-live`, and clearing feedback when the learner edits an answer.
- For `NEXT`, `SHOW ANSWER`, `RESET`, `CHECK ANSWERS`, audio controls, labels, inputs, selects, textareas, and dialogs, stop click or keyboard events from accidentally advancing the slide when needed. Reuse `data-no-slide-advance` where the current lesson supports it.
- For dialogs and teacher views, reuse the established `<dialog>` pattern with a `showModal()` path and an `open`/`hidden` fallback.
- For pair work or Student A/B activities, reuse the Lesson03/Lesson04 pair-number, role-selection, teacher-code, change-selection, and teacher-answer patterns before inventing a new system.

## Media Conventions
- Put lesson media in the current lesson's `assets/images`, `assets/audio`, or `assets/videos` folder.
- Optimize media for GitHub before referencing it. For speech audio, prefer a compact mono MP3 when quality remains clear.
- Add media placeholders only when the slide specification explicitly requires media and the final asset has not been provided.
- Placeholder labels must be clear, for example `IMAGE PLACEHOLDER - family tree`, `AUDIO PLACEHOLDER - listening 4.03`, or `VIDEO PLACEHOLDER - interview clip`.
- Do not generate missing media and do not add decorative placeholders just to fill space.

## Reuse Before Creating
- Prefer existing slide patterns: cover, objectives, grammar explanation/map, quick check, reference bank, listening activity, media activity, vocabulary grid/list, check-answer practice, pair speaking, information gap, Student A/B, teacher/testing mode, and homework launcher.
- Prefer existing generic helpers in the lesson (`CourseUtils`, slide store, progress, navigation, keyboard, font-size controls) over new globals.
- Do not extract shared CSS or JavaScript from existing lessons unless the user explicitly asks for an architecture refactor. Current lessons are large but working and self-contained.

## Validation
- After edits, run a static syntax check of inline scripts with Node when possible.
- Confirm slide count, required controls, required media paths, and requested interactive elements.
- Confirm no unrelated lesson content changed.
- Browser screenshots or DOM inspection are only required when the user explicitly asks for visual/browser QA.
