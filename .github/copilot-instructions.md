# Copilot instructions

## Project overview

This is a no-build, no-dependency space exploration quiz implemented entirely in `index.html`. The page contains the markup, inline CSS, the 10-question data set, and the quiz logic; opening the file directly in a browser is the normal way to run it.

The quiz is data-driven: `questions` holds each prompt, four answer strings, a zero-based `correct` answer index, and an explanatory `fact`. `renderQuestion()` rebuilds the answer buttons and updates the mission readout and progress. `selectAnswer()` tracks the current choice, `checkAnswer()` locks the answers and updates feedback and score, and `showResults()`/`restartQuiz()` manage the end and replay states. The mutable quiz state is held in `currentIndex`, `score`, `selectedIndex`, and `answered`.

## Build, test, and lint

There is no package manifest, build process, automated test runner, or lint command. Run the app by opening `index.html` directly in a browser; no server or dependency installation is needed.

For a focused manual smoke test after changing quiz behavior, exercise one correct and one incorrect answer, confirm score and progress updates, complete all 10 questions, check the results screen, and use Play again to verify reset behavior. Keyboard navigation between answers uses the arrow keys; answer buttons retain native Enter/Space activation.

## Code conventions

- Keep application changes self-contained in `index.html` unless the project gains a clear need for additional files or tooling. CSS, markup, question content, and JavaScript currently live together.
- Add or edit quiz content through the `questions` array. The `correct` field is a zero-based index into that question's `answers`; keep its fact and answer choices aligned.
- Keep quiz state transitions in the existing functions. `renderQuestion()` is the reset point for each question; answer selection, scoring, feedback, final results, and replay are handled separately.
- The script uses element IDs as DOM hooks. When changing markup, keep those IDs and their `document.querySelector()` references in sync; answer buttons are generated at render time.
- Preserve the accessible interaction pattern: answers are native buttons with `aria-pressed`, answer navigation supports arrow keys, feedback is announced through the live status region, and progress exposes its current value through `role="progressbar"` and `aria-valuenow`.
- Keep visual styling aligned with the CSS custom properties in `:root` and the `prefers-color-scheme: dark` override. Responsive layout and reduced-motion behavior are handled in the existing media queries.
