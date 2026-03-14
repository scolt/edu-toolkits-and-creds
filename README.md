# Quiz CLI

A lightweight command-line quiz application built with Node.js. It provides a simple interactive quiz experience using data stored in JSON, with utilities for colored output and terminal-based prompts. The app runs in the terminal and is driven by the files in the repository (index.js, src/, and data/questions.json).

## Features

- Interactive, terminal-based quiz experience
- Multiple categories of questions loaded from data/questions.json
- Configurable number of questions per run
- Colored output and progress display for a better UX
- Shows results and explanations for incorrect answers

## Tech stack & tools

- Node.js (ES Modules / "type": "module" in package.json)
- Built-in Node APIs (fs, readline, etc.)
- No external runtime dependencies declared in package.json
- MIT license

## Prerequisites

- Git — https://git-scm.com/
- Node.js (engine specified in package.json: >= 18.0.0) — https://nodejs.org/

Verify Node.js version:
```
node -v
```

## Installation

Clone the repository and run using Node.js. There are no project dependencies to install via npm for this repository as provided, but you can still use npm to run the included script.

```
git clone https://github.com/scolt/edu-toolkits-and-creds.git
cd edu-toolkits-and-creds
```

## Usage

Run the CLI using the package script or directly with Node:

- Using npm:
  ```
  npm start
  ```

- Direct with Node:
  ```
  node index.js
  ```

When started the CLI will:
- Load the question categories from `data/questions.json`.
- Prompt you to choose a category.
- Prompt you to choose the number of questions to attempt.
- Walk you through each question (selecting answers via numeric choices).
- Show a final score, performance message, and list incorrect answers with explanations.
- Offer an option to replay.

Example run (high-level):
```
$ npm start
# follow prompts: choose category, choose number of questions
# answer each question by entering the option number
# see final score, explanations for missed questions
```

## Adding or Editing Questions

Questions live in `data/questions.json`. The file structure is a top-level `categories` object. Each category key maps to an array of question objects.

Schema for each question object:
- `question` (string): The question text
- `options` (array of strings): The answer choices
- `answer` (number): The index (0-based) of the correct option in `options`
- `explanation` (string): Explanation shown when the question is answered incorrectly (optional but recommended)

Example snippet:
```json
{
  "categories": {
    "my-category": [
      {
        "question": "What is 2 + 2?",
        "options": ["3", "4", "5", "22"],
        "answer": 1,
        "explanation": "2 + 2 is 4."
      },
      {
        "question": "Which language runs in the browser?",
        "options": ["Python", "C++", "JavaScript", "Java"],
        "answer": 2,
        "explanation": "JavaScript is supported natively by browsers."
      }
    ]
  }
}
```

To add new categories or questions:
1. Open `data/questions.json`
2. Add a new key under `categories` for your category name, with an array of question objects following the schema above.
3. Save the file and run the CLI again.

Note: Keep the `answer` as a 0-based index corresponding to the `options` array.

## Project structure

- index.js
  - CLI entrypoint. Loads questions, prompts the user, orchestrates the quiz run.
- src/colors.js
  - ANSI color helpers and small convenience functions to colorize terminal output.
- src/input.js
  - Readline-based prompt utilities (prompt, select, confirm, pressEnter).
- src/quiz.js
  - Quiz logic and presentation: shuffling, tracking score, asking questions, rendering results.
- data/questions.json
  - JSON file containing quiz categories and questions.
- package.json
  - Project manifest and npm scripts (start script: `node index.js`).

This structure separates CLI orchestration (index.js), user input helpers (src/input.js), presentation/colors (src/colors.js), and core quiz logic (src/quiz.js). Tests are not included in the repository; adding tests should follow a similar separation (e.g., tests/ for unit tests that import src/ modules).

## Testing

No automated tests are provided in this repository.

Manual test / verification:
- Run `npm start` or `node index.js` and exercise the app via the prompts.
- To add automated tests, consider adding a `tests/` folder and using a test runner (e.g., Jest or Mocha) and mocking stdin/readline for integration tests.

## Contribution

Contributions are welcome. Suggested workflow:
1. Fork the repository.
2. Create a feature branch: `git checkout -b feat/my-change`
3. Make changes, update or add questions in `data/questions.json` if applicable.
4. Open a pull request describing your changes.

Notes:
- Keep changes focused and small per PR.
- If adding dependencies or changing runtime requirements, update `package.json` and document the change in the README.

## License

This project is licensed under the MIT License. See `package.json` for license metadata.

## Suggested future improvements

- Add automated tests for the Quiz class and input helpers.
- Add additional question types (multi-select, free-text) and validation.
- Persist high-scores and user history (local JSON or light database).
- Add CLI flags for non-interactive runs (e.g., choose category and question count via arguments).
- Add dependency management and linting (ESLint, Prettier) and a CONTRIBUTING.md for contribution conventions.

---