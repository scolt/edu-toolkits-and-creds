# Quiz CLI

Interactive command-line quiz game written in Node.js. The app loads a question bank from `data/questions.json`, lets you pick a category and question count, then walks you through the quiz while tracking your score. It uses ES Modules and Node’s built-in modules for file I/O and terminal input, with no external runtime dependencies. At the end of each round it prints a results summary and highlights any missed questions for review.

## Contents

- [Features](#features)
- [Used technologies](#used-technologies)
- [Project structure](#project-structure)
- [Setup instructions](#setup-instructions)
- [Getting started](#getting-started)
- [Usage examples](#usage-examples)

## Features

- **Category-based quizzes**: choose a category from the question bank (for example: JavaScript Basics, Node.js Fundamentals, General Programming).
- **Configurable quiz length**: play through all questions in a category, or a shorter set when the category has enough questions.
- **Interactive terminal UI**: numbered selections, prompts, and “press Enter to continue” pauses.
- **Scoring and review**: shows your final score and lists incorrect answers with the correct choice.
- **Readable, dependency-free output styling**: ANSI color helpers in `src/colors.js`.

## Used technologies

- **Node.js** (requires `>=18.0.0` per `package.json`): https://nodejs.org/
- **JavaScript (ES Modules)** (`"type": "module"` in `package.json`)
- **Node.js built-in modules**
  - `node:readline` for user input
  - `node:fs/promises` + `node:path` for loading `data/questions.json`
  - `node:url` utilities for resolving the current module directory
- **Node.js test runner** (script: `node --test`): https://nodejs.org/api/test.html

## Project structure

```
.
├── index.js
├── package.json
├── data/
│   └── questions.json
└── src/
    ├── colors.js
    ├── input.js
    └── quiz.js
```

- `index.js` — CLI entry point. Loads questions from `data/questions.json`, drives the main menu loop, and prints the banner/results.
- `data/questions.json` — Question bank grouped into `categories`. Each category has a `name` and a `questions` array.
- `src/` — Internal modules:
  - `src/input.js` — readline-based prompting helpers (`select`, `confirm`, `pressEnter`).
  - `src/quiz.js` — quiz engine (`Quiz` class): shuffles questions, asks questions, tracks answers/score, renders results.
  - `src/colors.js` — ANSI styling utilities used by the CLI.

### Notes on tests

- `package.json` provides a `test` script (`node --test`), but this repository currently does **not** include any test files.
- If you add tests, keep them in a consistent location/pattern (for example in a `test/` directory or as `*.test.js` files) so the Node.js test runner can discover them. Mixing many ad-hoc patterns is possible, but not recommended.

## Setup instructions

### Prerequisites

- **Git**: https://git-scm.com/
- **Node.js `>=18.0.0`** (includes npm): https://nodejs.org/

### Install

```bash
git clone <REPO_URL>
cd quiz-cli

npm install
```

> This project does not declare any `dependencies` or `devDependencies` in `package.json`. Running `npm install` is still a standard setup step and will validate your environment.

## Getting started

Run the CLI:

```bash
npm start
```

Other useful commands:

```bash
# Run the CLI directly
node index.js

# Run the test runner (no tests are currently present)
npm test
```

## Usage examples

### Play a quiz

1. Start the app: `npm start`
2. Choose a category when prompted.
3. Choose how many questions to answer.
4. Answer each question by entering the option number.
5. Review your score and any incorrect answers at the end.

### Add or edit questions

Edit `data/questions.json`.

- Categories live under `categories` (the object keys are used as category IDs).
- Each question object contains:
  - `question` (string)
  - `options` (string array)
  - `answer` (number; 0-based index into `options`)
  - `explanation` (string)
