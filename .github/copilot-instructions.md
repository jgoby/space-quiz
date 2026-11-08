# Copilot instructions

## Project overview

This is a no-build, no-dependency space exploration quiz implemented entirely in `index.html`. The page contains the markup, inline CSS, the 10-question data set, and the quiz logic; opening the file directly in a browser is the normal way to run it.

The quiz is data-driven: `questions` holds each prompt, four answer strings, a zero-based `correct` answer index, and an explanatory `fact`. The static HTML provides the quiz and results containers; `renderQuestion()` rebuilds the answer buttons and updates the mission readout and progress. `selectAnswer()` tracks the current choice, `checkAnswer()` locks the answers and updates feedback and score, and `showResults()`/`restartQuiz()` switch between completion and replay. The mutable quiz state is held in `currentIndex`, `score`, `selectedIndex`, and `answered`.

## Build, test, and lint

There is no package manifest, build process, automated test runner, or lint command. Run the app by opening `index.html` directly in a browser; no server or dependency installation is needed.

For a focused manual smoke test after changing quiz behavior, use the integrated browser or open `index.html` directly. Move focus through the answers with the arrow keys, select with Enter/Space or a pointer, exercise one correct and one incorrect answer, confirm score and progress updates, complete all 10 questions, check the results screen, and use Play again to verify reset behavior. There is no automated test runner or single-test command.

## Code conventions

- Keep application changes self-contained in `index.html` unless the project gains a clear need for additional files or tooling. CSS, markup, question content, and JavaScript currently live together.
- Add or edit quiz content through the `questions` array. The `correct` field is a zero-based index into that question's `answers`; keep its fact and answer choices aligned.
- Keep quiz state transitions in the existing functions. `renderQuestion()` is the reset point for each question; answer selection, scoring, feedback, final results, and replay are handled separately.
- Keep each question's four answers aligned with its `correct` index; only a correct selection increments `score`. Checking an answer disables all choices and reveals the correct one, including after an incorrect selection.
- Answer buttons are generated in `renderQuestion()`. The script uses element IDs as DOM hooks; when changing markup, keep those IDs and their `document.querySelector()` references in sync. Results markup is generated in `showResults()`.
- Preserve the accessible interaction pattern: answers are native buttons with `aria-pressed`; arrow keys move focus cyclically without selecting an answer; Enter/Space retains native button activation; feedback is announced through the live status region; and progress exposes its current question through `role="progressbar"` and `aria-valuenow`.
- Progress represents the current question (question 1 is 1 of 10), not only completed questions. Keep the visual bar and its accessible value synchronized.
- Keep visual styling aligned with the CSS custom properties in `:root` and the `prefers-color-scheme: dark` override. Responsive layout and reduced-motion behavior are handled in the existing media queries.
