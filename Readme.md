# README.md

1) High-level description of the application

Quiz CLI is an interactive command-line quiz game written in modern JavaScript (ES modules) for learning programming concepts. It loads question data from a JSON file, presents category and question-selection prompts, collects answers, shows explanations and a final score, and lets the user play again. The code demonstrates Node.js built-ins (fs/promises, readline), async/await, classes, array methods, and simple ANSI color utilities.

2) Features

- Interactive CLI with menus for:
  - Selecting a category (JavaScript Basics, Node.js Fundamentals, General Programming)
  - Choosing how many questions to answer (All / 3 / 5 where available)
- Randomized question order per quiz run (Fisher–Yates shuffle)
- Per-question selection by entering the option number
- Explanations for answers shown with results
- Score tracking and final results display
- ANSI-colored output via a small, dependency-free color utility
- Play again prompt to repeat quizzes without restarting the program
- Data-driven questions stored in data/questions.json for easy editing/extending

3) Used technologies (techstack, tools)

- Node.js (package.json requires Node >= 18.0.0)
- ES Modules (package.json "type": "module")
- Built-in Node APIs:
  - fs/promises for reading JSON data
  - readline for user input
  - path / url utilities for locating runtime files
- No external dependencies (colors implemented with ANSI escape codes in src/colors.js)

4) Project structure with explanation

Repository layout:
- index.js — Entry point and main application loop. Loads questions, drives interaction, and manages quiz sessions.
- package.json — Project metadata, scripts, Node engine requirement, and CLI configuration (ES module).
- data/
  - questions.json — All quiz content organized by categories. Each category has a name and an array of questions with options, answer index, and explanation.
- src/
  - colors.js — Small utility to colorize console output using ANSI escape codes. Provides convenience functions (success, error, info, highlight, etc.).
  - input.js — Input-handling helpers built on readline. Exports createInterface, prompt, select, confirm, pressEnter.
  - quiz.js — Quiz class and supporting logic (shuffle function, question flow, scoring). Responsible for asking questions and showing results.

Notes and recommendations:
- The project keeps core functionality inside src/*. That pattern is recommended for consistency (utilities, classes, and input handlers).
- There are no test files present in the repository; package.json provides a "test" script (node --test) but no test suite is included. Adding a tests/ folder with Node's test runner or another test framework is recommended if you introduce tests.
- A .DS_Store file is listed but is not relevant to functionality and can be ignored or removed.

5) Setup instructions (prerequisites and environment)

Prerequisites:
- Git (to clone the repository) — https://git-scm.com/
- Node.js 18 or newer (required in package.json) — https://nodejs.org/

Steps:
1. Clone the repository:
   - git clone <repo-url>
2. Change into the project directory:
   - cd edu-toolkits-and-creds
3. (Optional) Install Node modules:
   - npm install
   Note: This project has no external dependencies; npm install is not required for functionality but is a standard step if you add packages later.

Permissions:
- index.js includes a Unix shebang (#!/usr/bin/env node). On Unix-like systems you can make it executable (chmod +x index.js) and run it directly. Alternatively use npm start or node index.js.

6) Getting started guide (important commands and actions)

Common commands:
- Start the CLI via npm:
  - npm start
- Start the CLI directly with node:
  - node index.js
- Run the test script placeholder (no tests provided in repository):
  - npm test
  (This runs node --test; since there are no test files, it will not run any tests.)

Typical interactive flow after starting:
1. The app clears the terminal and shows the banner.
2. You are prompted to "Choose a category:" and shown numbered category options.
   - Select by entering the number for the category.
3. You are prompted "How many questions?" and select one of the available choices (All / 3 / 5).
4. The quiz starts. For each question:
   - Options are listed with numbers.
   - Enter the number corresponding to your chosen answer.
   - After each question (if more remain) press Enter to continue.
5. At the end, your results and explanations are displayed.
6. You are asked "Would you like to play again? (y/n):" — enter y or n.

Examples of usage

Example: run via npm
- npm start

Example: run directly
- node index.js

Example CLI session (illustrative):
- App shows banner
- Prompt: Choose a category:
  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming
  Enter: 1
- Prompt: How many questions?
  1. All questions
  2. 3 questions
  3. 5 questions
  Enter: 2
- Starting quiz...
- (Press Enter)
- Question 1:
  1. var
  2. let
  3. const
  4. define
  Your choice (enter number): 3
- (shows whether correct and the explanation)
- (Press Enter to continue)
- ...repeat until complete
- Results displayed: score and explanations
- Play again? (y/n): n

Editing or adding questions
- Questions live in data/questions.json. Each category has this structure:
  {
    "categories": {
      "categoryId": {
        "name": "Category Display Name",
        "questions": [
          {
            "question": "Question text",
            "options": ["opt1", "opt2", ...],
            "answer": <index of correct option starting from 0>,
            "explanation": "Explanation text"
          },
          ...
        ]
      },
      ...
    }
  }
- Adjust or add categories/questions as needed. Keep answer indices zero-based.

License
- MIT (see package.json)

If you plan to extend this project, recommended next steps:
- Add automated tests under a tests/ directory and update the test script.
- Add CLI flags to skip prompts (for scripting) or to select categories via arguments.
- Add persistence (saving high scores) or timed questions for more advanced gameplay.
