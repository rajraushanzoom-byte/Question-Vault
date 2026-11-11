# Question Vault

**Every question you meet, turned into skill.**

Question Vault is a single-file web app for coding practice. Paste a question and it becomes a full practice room. Test cases are written for you, your solution is judged however you choose to solve it, and your library grows into a timed mock exam.

Everything lives in one file, `index.html`. There is no server, no build step and no install.

---

## Features

| Feature | What it does |
|---|---|
| **Question library** | Save questions in folders you name yourself. Filter by difficulty, status or search text. Mark questions as important. |
| **AI test cases** | Paste a question and the AI suggests test cases, including edge cases. It can also fill in expected outputs from your reference solution. |
| **Function-style questions** | For LeetCode-style "write a function" questions, a hidden driver reads the input, calls your function and prints the result. You only write the function. |
| **AI Judge** | Runs your code on saved and freshly generated tests. Any valid approach passes if the output is right. You get Accepted or Wrong Answer, per-case input, expected and actual output, the detected approach, and time and space complexity. |
| **Predict and Review** | The AI can predict a program's output or review your answer and explain likely bugs without writing the full fix. |
| **Mock exams** | Pick folders, difficulty and a question pool. Sit a timed exam built from your own library. |
| **Web questions** | HTML and CSS questions get their own checks and preview instead of the code runner. |
| **Many languages** | Python, Java, C++, HTML, SQL or any language you type in. |
| **Private by default** | Questions, progress and settings are saved in your browser's `localStorage`. |

---

## Quick start

1. Download `index.html`.
2. Open it in any modern browser (Chrome, Edge, Firefox or Safari).
3. Open the AI settings and add an API key (see below).
4. Click **Add a question**, paste a question and let the AI suggest tests.
5. Open the question in **Library**, write your solution and click **AI Judge**.

No internet is needed to browse your library. The AI features and the code runner need a connection, unless you use a local model such as Ollama.

---

## Setting up the AI

The app talks to the AI provider you choose, directly from your browser, using your own API key.

Supported providers:

- Google Gemini
- OpenAI
- Anthropic (Claude)
- OpenRouter
- Groq (free tier, very fast)
- Mistral
- DeepSeek
- Ollama (runs on your computer)
- Custom (any OpenAI-compatible server)

Steps:

1. Open the AI settings in the app.
2. Choose a provider. Groq or Gemini are good starting points because they have free tiers.
3. Use the **Show me how** guide to get a key, then paste it in.
4. Pick a model, or keep the default.

Your key is stored only in your browser. It is sent only to the provider you selected.

---

## Setting up the code runner

Code is executed through a Judge0-compatible service. The default address is:

```
https://ce.judge0.com
```

You can change the address, or add a token, in the runner settings. To keep things private or avoid rate limits, you can point it at your own Judge0 instance.

If no runner is available, the app can fall back to AI-predicted output. These results are less reliable than real execution, so check them if something looks odd.

---

## How the AI Judge works

1. The AI reads the question and writes new test cases.
2. These are merged with your saved tests, and duplicates are dropped.
3. Your code runs on every case.
4. Expected output comes from running your saved **reference solution**. If you did not save one, the AI's expected output is used.
5. Outputs are compared with whitespace ignored.
6. The AI names your approach, estimates complexity and explains any failure.
7. If every case passes, the question is marked solved.

Because the comparison is on output, a loop, recursion, hash map or built-in method are all accepted if the result is correct.

---

## Tips

- Save a **reference solution** with each question. It gives the most trustworthy expected outputs.
- Mark a few cases as hidden so you can't just fit your code to the visible ones.
- Keep one folder per topic (arrays, strings, SQL) so mock exams are easy to build.
- Use a different browser profile for a separate library, since data is stored per browser.

---

## Limitations

- Data is stored in your browser. Clearing site data deletes your library, so back it up if it matters.
- AI-written tests and expected outputs can be wrong. Treat them as a strong guide, not proof.
- The public Judge0 service has rate limits and can be slow at busy times.
- A key entered in the browser is visible to anyone using that browser, so use keys with spending limits.

---

## Tech

- Plain HTML, CSS and JavaScript in one file, with no dependencies
- Storage: `localStorage`
- Code execution: Judge0-compatible API
- AI: provider APIs called from the browser

---

## Project structure

```
index.html   the whole app (markup, styles and scripts)
README.md    this file
```
