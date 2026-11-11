# Question-Vault

# Question Vault

**Your personal coding gym.** Paste in any question you come across, practice it in a real editor, and turn your whole collection into timed mock exams.

Live site: https://rajraushanzoom-byte.github.io/MOCK-TEST/

---

## Why I built this

While studying, I kept running into the same problem: questions were scattered everywhere. Some were in assignment PDFs, some in screenshots, some in random notes. I could never go back and practice them properly, and I had no way to test myself on only the ones I'd got wrong.

Question Vault fixes that. You save a question once, and the app turns it into a proper practice room with an editor, test cases, hints and a hidden solution. When you've collected enough, you can build a mock exam out of your own library and see how you really do.

It is one single `index.html` file. There is no build step, no framework and no server of my own. You open it, or host it on GitHub Pages, and it works.

---

## What it can do

### 1. Library (the home screen)

- Questions live in **folders and sub-folders**, shown as a tree on the left. A folder can be tied to a language, so new questions inside it default to that language.
- **Search** by title, topic or question text.
- **Filter** by difficulty (easy / medium / hard) and by status (all, marked important, unsolved, solved).
- Important questions get a **highlighter-yellow mark**, like you'd do on paper.
- A progress bar at the top shows how many questions you've solved.

### 2. Adding a question

Only two things are required: the folder (or language) and the question text. Copy the question from wherever you found it and paste it in. Everything else is optional:

- title, topic, difficulty
- starter code (boilerplate shown in the editor when you practice)
- a saved solution and an explanation
- hints, one per line
- test cases (visible or hidden)
- for CSS questions, the HTML that your CSS gets applied to

Code wrapped in triple backticks shows up as a proper code block, and single backticks give inline code.

There's also a **"Save and add another"** button for when you're adding a batch.

### 3. Practice mode

Opening a question gives you:

- the question, with example input/output taken automatically from the first two visible test cases
- a **syntax-highlighted code editor** (a transparent textarea over a highlighted layer, so it feels like a normal editor)
- a **terminal panel** where you can type input, run your code, and see real output
- a **Run tests** button that checks your code against every test case. Hidden tests only show pass or fail, like a real exam portal.
- **hints that unlock one at a time**
- a **solution that stays hidden** until you confirm you want to see it
- "I got it" / "Needs more practice" buttons that mark the question solved, or mark it important to revisit

Some nice details:

- You can **solve the same question in a different language** than the one it was saved in. The tests stay the same and your code is saved separately for each language.
- Your draft is saved as you type, so closing the tab doesn't lose your work.
- `Alt + ←` and `Alt + →` jump between questions.
- If you only need to write a function (not a whole program), the app adds a hidden runner behind the scenes that reads input, calls your function and prints the result. It can generate this runner itself for JavaScript, Python, Java, C++, C and C#.

### 4. Mock exams

This is the main reason the whole thing exists.

1. **Pick folders** to draw questions from.
2. Narrow by difficulty, and by pool: everything, only important ones, only unsolved ones, or only the ones you **missed in a previous exam**.
3. Choose **random mix** (you set how many) or **I will choose them** (manual picking).
4. Set a **timer** in hours, minutes and seconds, use a preset (15, 30, 45, 60, 90, 120 minutes), or turn the limit off and let the clock count up.
5. Start. You can pause the timer. If you close the page in the middle of an exam, it restores where you left off.

When you finish, the app marks your work in two stages:

- Questions **with test cases are marked automatically** by running your code against them.
- For the rest, you compare your answer with the saved solution and mark it yourself as Correct, Partly right or Wrong. If you've set up AI, there's a "Mark with AI" button that suggests a mark, and you can always override it.

Scoring: Correct = 1 mark, Partly right = 0.5, Wrong = 0. At the end you see:

- your percentage and marks
- time used
- a breakdown **by language**
- a question-by-question list
- a **"Retry the missed ones"** button that starts a new exam from only your wrong answers

Recent attempts are kept in a history list on the setup screen.

### 5. AI (optional, and bring your own key)

The app does not ship with any AI key, and nobody has to use AI. If you want it, open **AI setup** and paste in your own API key. Supported providers:

| Provider | Notes |
|---|---|
| Google Gemini | Has a free tier |
| OpenAI | Paid account |
| Anthropic (Claude) | Paid account |
| OpenRouter | One key for many models, some free |
| Groq | Fast, free tier |
| Mistral, DeepSeek | Own accounts |
| Ollama | Runs on your own computer, no key |
| Custom | Any server that speaks the OpenAI chat format (LM Studio, vLLM, Together and so on) |

Each provider keeps its own key and model, so you can switch back and forth. There are **Test connection** and **Load my models** buttons to help sort out the "which model name works for my key" problem, and a step-by-step guide for getting an API key from each provider.

What AI is used for:

- **Improve with AI:** rewrites a rough pasted question into a clean exam-style question (title, description, Input, Output, Constraints), picks difficulty and topic, writes a solution, explanation, four beginner-friendly hints and test cases. It can run automatically the moment you paste a new question, and there's an **Undo AI changes** button.
- **Suggest test cases** for a question.
- **Mark with AI** during mock exams.
- **Translate a saved solution** into the language you chose to solve in.
- Multiple-choice and theory questions are recognised and formatted properly too.

AI is deliberately not the thing that decides whether your code passes. When a question has test cases, your code is **actually run** and the output is compared with the expected output. The AI-marking prompt is also written to accept any valid approach, not just the one that matches the reference solution.

### 6. How code actually runs

| Language | How it runs |
|---|---|
| JavaScript | For real, in your browser (in a Web Worker) |
| Python | For real, in your browser using Pyodide (downloaded from a CDN the first time, which takes a few seconds). Falls back to the online compiler if it can't load. |
| Java, C++, C, C#, Go, Rust, Kotlin, PHP, Ruby and others | Sent to an online compiler. It tries **Judge0** first (the public `ce.judge0.com` by default) and falls back to **Wandbox**. |
| HTML / CSS | Rendered inside a hidden sandboxed iframe, and each test is a small JavaScript expression checked against the finished page |

You can point the app at your own Judge0 server (with an optional access token) in the Code runner section of AI setup. There's also an opt-in checkbox that lets the AI *predict* output if no compiler can be reached. It's off by default because predicted output can be wrong.

Output comparison ignores extra spaces and trailing blank lines, so you aren't failed for invisible whitespace.

### 7. Accounts and cloud saving (optional)

- **Without an account**, everything is stored in your browser's `localStorage`.
- **With Google sign-in** (Firebase Auth + Firestore), your folders, questions and history sync to your account and follow you to any device. There's a small status indicator showing "Saving…", "Saved to your account" or a retry message when you're offline.
- When you sign in for the first time and the browser already holds questions, the app asks whether to upload them to your new account.
- Saves are batched and only changed items are sent, so it stays fast with a big library.

### 8. Backup and restore

Under **Backup and restore** on the library page you can download a `question-vault-backup.json` file, copy the backup as text, and restore from either a file or pasted text. If you aren't signed in, please use this regularly, because clearing your browser data would otherwise wipe the library.

---

## Getting started

**Just use it:** open the live site above.

**Run it locally:**

1. Download `index.html`.
2. Double-click it, or serve the folder with anything simple, for example:
   ```bash
   python -m http.server 8000
   ```
3. Open `http://localhost:8000`.

**Host it yourself on GitHub Pages:**

1. Put `index.html` in a repository.
2. Go to *Settings → Pages* and publish from the main branch.
3. Visit the URL GitHub gives you.

A short **Getting started guide** appears at the top of the library for new users, and can be closed or reopened with the button near Backup and restore.

---

## Setting up your own Firebase (only if you fork this)

The Google sign-in feature is wired to my Firebase project. If you fork the project and want your own accounts and data, edit `FIREBASE_CONFIG` near the bottom of the script:

1. Create a free Firebase project.
2. Turn on **Google** as a sign-in method.
3. Create a **Firestore** database.
4. Add your site's domain (for example `yourname.github.io`) to the authorised domains.
5. Paste your web app config into `FIREBASE_CONFIG`.
6. Set Firestore rules so each person can only read and write their own data:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{uid}/{document=**} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }
   ```

The Firebase web config is not a secret. The security comes from those rules, so please don't skip step 6.

If the config is missing, the app simply keeps working as a guest-only app.

---

## A few honest notes

- **Your API key stays in your own browser** (`localStorage`). Never paste it into the code or push it to GitHub.
- **Questions you paste are sent to whichever AI provider you choose.** Some free tiers may use that data to improve their products, so avoid private material.
- Compiled languages need an **internet connection**, because they run on a public online compiler. The free public servers can be slow or rate-limited at busy times.
- AI-written solutions, hints and test cases can be wrong. The app tries to verify generated solutions by running them against the generated tests, but it's still worth glancing over anything the AI produced.
- Because it is a single file of roughly 3,500 lines, it's easy to deploy but not the easiest thing to read. If it grows more, splitting the CSS and JavaScript into separate files would be a sensible next step.

---

## How the code is organised

Everything lives in `index.html`, in three parts: the styles, the markup for each screen, and one script. The script is divided with comment banners, roughly in this order:

1. **Helpers**: DOM builder `h()`, timers, toasts, shuffling
2. **Languages and state**: language list, colours, `localStorage` keys, the `S` state object, data cleaning (`norm`, `normFolder`)
3. **Folders**: tree helpers (`kids`, `pathOf`, `subtreeIds`, `countIn`)
4. **Rich text and syntax highlighting**: a small hand-written highlighter for many languages, plus HTML and CSS
5. **Code editor**: highlighted layer under a transparent textarea, with tab and bracket handling
6. **AI layer**: provider table, `askAI()`, JSON parsing, error handling
7. **Running code**: browser workers for JS and Python, Judge0 and Wandbox, and the auto-generated function runners (`awJs`, `awPy`, `awJava`, `awCs`, `awCpp`, `awC`)
8. **Terminal and workspace**: console, input box and test results
9. **AI prompts**: improve, hints, tests, review and driver-fix prompts
10. **Navigation and library**: views, folder actions, question list
11. **Practice, add/edit and backup**
12. **Mock exam**: setup, run, marking and results
13. **Accounts and cloud saving**: Firebase auth and Firestore sync
14. **Guides and `init()`**: wiring everything together

**Stack:** plain HTML, CSS and vanilla JavaScript. Fonts come from Google Fonts (Bricolage Grotesque, IBM Plex Sans, JetBrains Mono). Pyodide and Firebase are loaded from CDNs only when needed. No build tools, no npm.

**Data model.** A question stores its language, title, difficulty, topic, statement, starter code, solution, hidden driver code, explanation, hints, tests (`input`, `expected`, `hidden`, and `check` for web questions), HTML preview, flags for important and solved, your drafts per language, attempt count and last result, and its folder. A folder stores a name, its parent, an optional language and a created time.

---

## Roadmap ideas

- Import questions in bulk from a file
- Spaced repetition for questions you keep missing
- Streaks and a simple activity calendar
- Splitting the single file into modules
- Shareable question packs between friends

---

## Credits

Built by Raj as a learning project, with help from AI tools along the way. Thanks to the free services that make it possible: Judge0, Wandbox, Pyodide and Firebase.

If you find a bug or have an idea, feel free to open an issue.
