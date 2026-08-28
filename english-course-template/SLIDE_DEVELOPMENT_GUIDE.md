# English Course Slide Development Guide

Use this guide to create future slides with less repeated prompting. The existing lessons are the source of truth.

## Where To Work
- Add new lesson slides inside `english-course-template/LessonNN/index.html`.
- Put lesson assets in `LessonNN/assets/images`, `LessonNN/assets/audio`, or `LessonNN/assets/videos`.
- Put homework pages in `LessonNN/workbook/`.
- Do not touch older lessons unless the request explicitly asks for it.

## Standard Slide Shape
Use the current deck pattern:

```html
<section class="slide example-slide" id="slide-example" data-slide aria-labelledby="slide-example-title" tabindex="-1" hidden>
  <header class="slide-header">
    <p class="slide-kicker">Lesson N</p>
    <h2 id="slide-example-title">Slide Title</h2>
    <p class="slide-subtitle">Short instruction or purpose.</p>
  </header>

  <div class="slide-content">
    <!-- requested slide content -->
  </div>

  <footer class="slide-footer">
    <div class="slide-progress" data-slide-progress role="progressbar" aria-label="Lesson progress"><span></span></div>
    <p class="slide-count" data-slide-count>Slide N / N</p>
  </footer>
</section>
```

The runtime updates the real slide count and progress.

## Reusable Patterns Already Present
- Cover slide: Lesson01/02/03/04/05 first slide.
- Lesson objectives: Lesson01 slide 2, Lesson02 slide 2, Lesson05 slide 2.
- Grammar explanation/map: Lesson01 grammar slides, Lesson04 present simple slides, Lesson05 slide 4.
- Quick check with `NEXT` and `SHOW ANSWER`: Lesson04 present simple/negative, Lesson05 slide 4.
- Check-answer practice with `data-answer`: Lesson03 form/listening/practice slides, Lesson04 jobs/listening/checklist slides, Lesson05 slide 5.
- Pair number and Student A/B activity: Lesson03 mystery bag, Lesson04 office mystery and guess job.
- Teacher answer dialogs: Lesson03 mystery bag, Lesson04 office mystery and guess job.
- Reference bank: Lesson04 grammar/vocabulary bank, Lesson05 family words bank.
- Media activity: Lesson02 listening slides, Lesson03 video/listening, Lesson05 slide 5.
- Homework launcher: final slide pattern in each lesson.

## Naming
- Use semantic names scoped to the slide or activity.
- IDs: `slide-family-tree-richard`, `slide-possessive-grammar-map`.
- Classes: `family-tree-slide`, `grammar-map-slide`, `family-check-button`.
- Data attributes: `data-family-tree-check`, `data-family-check-answers`.
- JS functions: `createFamilyTreeCheck(root)`, `createPossessiveQuickCheck(root)`.
- Avoid generic data attributes for slide-specific behavior unless the lesson already has a generic helper for them.

## Interactions
- Keep slide-specific JavaScript inside one IIFE and expose one namespaced initializer on `window`.
- Call the initializer from the existing lesson boot function.
- Use `event.stopPropagation()` for activity buttons and audio/video controls that sit inside clickable slide areas.
- Use `aria-live` for feedback that changes after checks or answer reveals.
- Clear correct/incorrect feedback when the learner edits an answer.
- Reuse existing `is-correct`, `is-incorrect`, `hidden`, `aria-invalid`, and feedback styles where compatible.

## Media
- If the final asset is provided, optimize it and place it in the lesson asset folder.
- For speech audio, a mono MP3 at a low bitrate is usually enough when still clear.
- If media is required but absent, create only the needed placeholder and label it clearly:
  - `IMAGE PLACEHOLDER - [purpose]`
  - `AUDIO PLACEHOLDER - [purpose]`
  - `VIDEO PLACEHOLDER - [purpose]`
- Do not add media or placeholders when the slide does not require media.

## Minimal Diff Checklist
- Add only the requested slide(s).
- Reuse nearby CSS and JS patterns before creating new ones.
- Keep new CSS scoped to the new slide unless a tiny generic addition is obviously safe.
- Do not rename existing classes/functions or move large blocks.
- Do not rewrite old slides for consistency.
- Validate inline script syntax, slide count, required media paths, and required interactive controls.

## Deferred Improvements
- A shared runtime or extracted base CSS could reduce duplication across lessons, but existing lessons are self-contained and working. Do not extract them during normal slide creation.
- Generic helpers for check-answer and dialog behavior would be useful later, but introduce them only when a new task benefits directly and the diff remains small.
