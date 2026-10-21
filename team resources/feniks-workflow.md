# How to Use Feniks — Phase-by-Phase Guide

Print this. Keep it next to your laptop. You do NOT need to be an AI expert.

---

## Before you start: the 3 rules

1. **Feniks can read your files.** Tell it the path — e.g. "read `02-data-pack/C-crime/crime_subset.csv` and show me the columns." You don't need to copy-paste data.
2. **Run every line of code Feniks gives you.** If it doesn't run, paste the error back and say "fix this."
3. **Trust the data, not the AI.** If a number Feniks gives you doesn't match what you see in your dataframe, the data wins.

---

## How to use Feniks (60-second crash course)

You have **two windows** open:
- **OpenCode** (terminal app) — this is where you talk to Feniks. Type instructions, it reads/writes your files.
- **Jupyter** (browser) — this is where you run and see your notebook output.

**How it works:**
- In OpenCode, type what you want in plain English.
- Feniks (via OpenCode) can **read your files, write code, edit your notebooks, create new files, and run commands** — all on your local machine.
- Examples:
  - "Read `02-data-pack/C-crime/crime_subset.csv` and tell me the columns and row count."
  - "Add a cell to `03-team-resources/starter_crime.ipynb` that charts crime type by month using plotly."
  - "Create a Streamlit app that lets users search crime by LSOA name."
  - "This cell throws a KeyError on 'month' — fix it."
- Switch to Jupyter, run the cell, see the result.
- If it errors, go back to OpenCode, paste the error, say "fix this."

**You don't need to:**
- Copy data between files
- Manually manage file paths
- Write boilerplate code
- Know the exact pandas/plotly syntax
- Switch between apps to edit files — OpenCode does it for you

---

## Phase 1: Define (0:14–0:28)

**Your job (human):** Fill the Problem Canvas. Pick your user, question, archetype, dataset.

**Feniks can help with:**

| You want to... | Paste this into Feniks |
|---|---|
| Brainstorm citizen users for a dataset | "I have UK [house price / food hygiene / crime] data. List 5 specific citizen users who would genuinely use a tool built from this, and the one question each would ask." |
| Pick between archetypes | "I want to help [user] answer [question] using [dataset]. Should I build a dashboard, a search tool, or a predictor? Give me a one-line reason." |
| Sharpen your problem statement | "Rewrite this as a one-line problem statement a judge would understand: [your draft]" |

**Do NOT use Feniks for:** deciding what problem to solve. That's your team's call.

---

## Phase 2: Data dive (0:28–0:43)

**Your job (human):** Open your starter notebook, run the first cells, find 3 data facts.

**Feniks can help with:**

| You want to... | Paste this into Feniks |
|---|---|
| Understand the data dictionary | Paste the contents of your `data_dictionary.md` and ask: "Summarise the 3 most important quirks I need to know before analysing this." |
| Write a sanity check | "Write 3 pandas one-liners that check: (1) any negative prices, (2) dates before 1995, (3) duplicate postcodes. My dataframe is `df`." |
| Explain a weird value | "My `date` column shows values like `19950101`. What format is this and how do I parse it with pandas?" |
| Fix an error | Paste the full error message + the cell code. Ask: "Explain this error in one sentence and give me the fix." |

**Verify:** After any Feniks-generated check, look at the actual output. Does the number make sense?

---

## Phase 3: Build (0:43–1:43)

**Your job (human):** Build ONE thing. One chart, one search, one prediction. Done beats perfect.

**Feniks can help with:**

### Dashboard teams

| Step | Paste this |
|---|---|
| Plan your views | "I'm building a dashboard for [user] using [dataset]. Suggest exactly 3 charts. For each: chart type, x-axis, y-axis, and the question it answers." |
| Generate a chart | "Write plotly code for a [line/bar/scatter] chart from my dataframe `df`. X = [column], Y = [column], colour by [column]. Add a title." |
| Make it look presentable | "Add a title, axis labels, and remove the legend from this plotly chart: [paste your code]" |

### Search tool teams

| Step | Paste this |
|---|---|
| Write the search logic | "Write a function `search(df, query)` that filters `df` where [column] contains `query` (case-insensitive) and returns the top 10 rows sorted by [column]." |
| Handle no results | "What should my search tool show when there are 0 matches? Give me a 2-line pandas + print solution." |
| Wrap in Streamlit (stretch) | "Convert this search function into a minimal Streamlit app with a text_input and a dataframe display. Keep it under 20 lines." |

### Predictor teams

| Step | Paste this |
|---|---|
| Build a baseline | "Using `df`, write a baseline predictor for [target] that just returns the median of [target] grouped by [column]. Show me the MAE." |
| Add a simple model | "Now fit a sklearn LinearRegression on [features] to predict [target]. Show MAE and compare to my baseline. Is it actually better?" |
| Predict one example | "Use my fitted model to predict [target] for: [example input]. Show which features contributed most." |

### Everyone: when code breaks

```
Paste: the error message + the code that caused it
Ask:   "Fix this. Give me only the corrected code, no explanation."
```

If it's still broken after 2 attempts, **simplify**. Cut a feature, drop a column, use a smaller chart. Ask Feniks: "Give me the simplest possible version of this that still works."

---

## Phase 4: Pitch prep (1:43–1:50)

**Your job (human):** Rehearse. Make the demo deterministic (run it clean one final time).

**Feniks can help with:**

| You want to... | Paste this |
|---|---|
| Draft your 2-min pitch | "Write a 2-minute pitch (max 150 words) for: [user] + [tool] + [one insight from your data] + [next step]. Tone: confident, plain English, no jargon." |
| Find your "so what" | "My tool shows [X]. What is the ONE sentence a citizen would say after seeing it? Make it punchy." |
| Prepare for judge Q&A | "A judge might ask: 'How do I know this is accurate?' Give me a 2-sentence honest answer based on [your data source + method]." |

---

## Quick reference: what to paste as context

Feniks works better when you give it context. Before asking, paste:

- **Column names:** `df.columns.tolist()` output
- **A sample:** `df.head(3).to_string()` output
- **Your error:** the full red text from Jupyter
- **Your goal:** one sentence — "I want to show X to Y"

You don't need to paste the whole dataset. Column names + 3 rows + your question is enough.

---

## When to STOP using Feniks

- You've asked the same thing 3 times and it's still wrong → simplify the task.
- The answer is a number → verify it against your data before using it.
- You're deciding what to build → that's a team conversation, not an AI question.
- You have 10 minutes left → stop building, start rehearsing the demo.
