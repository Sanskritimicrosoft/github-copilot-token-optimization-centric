# Fusion lab · Same task, two bills

| | |
|---|---|
| **Time** | 20 minutes |
| **Cost** | About 12–25 AI credits (≈ $0.12–$0.25) per person, depending on the model you pick for Run A |
| **Before you start** | [Lab 0](../README.md#lab-0--get-set-up-5-min) is done: Copilot CLI is open in **your own copy** of this repo and `/usage` responds |

**What you'll do.** Give Copilot CLI one read-only task twice: explain this repo's dashboard app to a new teammate. First on one strong model, then on **Copilot Fusion**. After each run you score the answer and read the meter. Then you put the two bills side by side.

**What you'll take away.**

- How to read what a session really cost, with `/usage`.
- What Copilot Fusion does: it picks a model for each task and bills only what it used.
- How to tell a real saving (same quality, fewer credits) from a false one (cheaper, but you redo the work).

> This is an observation lab, not a race. Your numbers will differ from your neighbour's. Write down what *you* see.

---

## Step 0 · Get ready (1 min)

If Copilot CLI is open, close it:

```text
/exit
```

Every run starts in a **brand-new session**. That is the fair reset: the meter starts at zero and both runs get the same cold start. Use `/exit` and a new `copilot` command between runs, not `/clear`: `/clear` keeps the same session, so `/usage` would keep counting both runs.

This is the task. Send it **word for word** in both runs. Use the copy button on the block; it is one line on purpose, so it pastes as one message:

```text
Summarise the Incident Console app in console/ for a developer who joins the team tomorrow: what it shows, how the files in console/src fit together, where the alert thresholds live, and how to run it and its tests. Flag anything that looks like a bug. Read only what you need. Do not edit files, and do not run the app or its tests. Max 200 words.
```

## Step 1 · Run A: one strong model for everything (7 min)

Start a fresh session with a safety cap of 60 AI credits per response:

```bash
copilot --max-ai-credits 60
```

Open the model picker:

```text
/model
```

Run A model: pick GPT-6.1 Sol. If it isn't in your list, pick Claude Opus 5.5. If neither is there, press Shift+Tab in /model to group models by category, and pick any model under Powerful. Write its name down.

Paste the prompt and press **Enter**. While it works, watch the timeline: every file it opens joins the context, and the context is sent again on every later step.

If Copilot asks permission to run a command, say **yes** to read-only commands (`ls`, `cat`, `grep`, `find`) and **no** to anything that edits files or runs `node`.

When the answer lands:

1. **Score it** against the [answer key](#answer-key): one point per line, plus ★ if it spots the bug.
2. **Read the meter:** type `/usage` and write down the `AI Credits` figure and the model row.
3. **Close the session:** `/exit`

> **How to read `/usage`**
>
> ```text
> Changes    +0 -0                        ← files changed: must stay +0 -0
> AI Credits <credits> (<time>)           ← what this run cost: write it down
> Tokens     ↑ <in> (<cached>, <written>) • ↓ <out>
>   <model> ↑ … • <credits> AIC           ← the model you were billed for
> Plan       … % used                     ← your monthly allowance: ignore it here
> ```

## Step 2 · Run B: same task, Copilot Fusion (5 min)

Start a second fresh session, this time on Copilot Fusion at the **Standard** effort level:

```bash
copilot --model fusion --fusion-tier standard --max-ai-credits 60
```

Check that the status line under the prompt box says Copilot Fusion. *(Prefer the picker? Start plain `copilot`, run `/model` and choose **Copilot Fusion**, then **Standard**.)*

Paste the **same** prompt. Before it starts work, Fusion tells you which model it picked and why, for example *"Copilot Fusion selected <model> since the task has medium complexity."* Write that model down.

Then, as before: **score** the answer, run `/usage`, write down the credits and the model row, and `/exit`.

## Step 3 · Compare and share (5 min)

Fill this in, on paper or in a scratch file:

| | Run A · strong model | Run B · Fusion Standard |
|---|---|---|
| Model (from `/usage`) | | |
| AI credits | | |
| Score (out of 5, ★ bonus) | | |
| Felt fast or slow? | | |

Your saving: **(A − B) ÷ A × 100%**.

| What you see | What it tells you |
|---|---|
| Fusion cheaper, same score | The strong model was overkill for this task. Routing paid off. |
| Fusion cheaper, lower score | A cheap answer is no saving if you have to redo the work. Try Fusion **High** on harder tasks. |
| About the same | Fusion judged this task worth a strong model, and billed only the model it used. |
| Run A cheaper | Note it and share it. That is real evidence too, and the room wants to see it. |

Post your result line in the session chat so we can compare the whole room:

```text
A: <model> <credits> cr <score>/5 · B: Fusion → <model> <credits> cr <score>/5
```

> **Price note.** Until 30 November 2026, paid Copilot plans get 30% off model costs when using Copilot Fusion, so part of today's gap is that promotion. The comparison that lasts is the one after it ends.

### Answer key

<details>
<summary>Open when you score</summary>

One point each:

1. The entry point is `console/src/dash.mjs`, the render loop (`--once` prints a single frame).
2. The metrics are simulated but deterministic: a seeded generator in `metrics.mjs` (seed 42).
3. The gauge thresholds live in `thresholds.mjs` (`THRESHOLDS` and `statusFor()`).
4. Run it with `node console/src/dash.mjs`; test it with `node --test console/test/*.test.mjs`.
5. The screen shows CPU and MEM gauges, a REQ/S sparkline, a services table and a rolling log.

★ **Bonus:** it spots that the CPU critical threshold is `8.0` instead of `80`. Because the critical level is checked first, the CPU gauge is always red and the log fills with alerts. The bonus only counts if the agent found it in the code, not in these lab pages. *(Don't fix it here. That is [Lab 1](1-size-limit-record.md).)*

</details>

### Our dry run

<details>
<summary>Open after you have filled in your own table</summary>

Run on 23 November 2026, same prompt, same repo:

| | Run A | Run B |
|---|---|---|
| Model | GPT-6.1 Sol | Copilot Fusion Standard, which picked GPT-6 Luna ("medium complexity") |
| AI credits | 12.03 | 0.39 (0.55 without the Fusion promotion) |
| Files changed | 0 | 0 |

Fusion's answer scored 5/5 plus the bonus in 167 words. It also explained why the tests miss the bug: they check sample values, not the exported CPU setting. Saving: 96.8%.

</details>

---

## Finished early?

Pick any of these. Each one stands alone.

| Extra | Time | What you'll learn |
|---|---|---|
| [Run C · Turn the dial up](#run-c--turn-the-dial-up) | 5 min | What Fusion **Max** adds, and what it costs |
| [Run D · The cheapest single model](#run-d--the-cheapest-single-model) | 5 min | Whether "cheapest" beats "routed" once you count quality |
| [Run E · Where the tokens go](#run-e--where-the-tokens-go) | 5 min | What fills the context window before you type a word |
| [Lab 1 · Size it, cap it, record it](1-size-limit-record.md) | About 20 min | Fix the bug you just found, inside a credit budget |

### Run C · Turn the dial up

```bash
copilot --model fusion --fusion-tier max --max-ai-credits 60
```

Same prompt. Count the model rows in `/usage` now: at Max, Fusion can have one model draft while others review. Did the score move? Did the bill? For a read-and-explain task, extra reviewers rarely earn their credits. For a hard bug they might.

### Run D · The cheapest single model

Start a fresh `copilot --max-ai-credits 60`, run `/model` and pick a model from the *Lightweight* category (for example a "mini", "Luna" or "Haiku" model). Send the same prompt. Fusion is not trying to be the cheapest possible run; it is trying to meet the quality bar for the least it can. Where does the small model land on cost *and* score?

### Run E · Where the tokens go

In our dry run, Run A read about 184 tokens for every token it wrote. Most of the bill is context, not the answer. Start a fresh `copilot` and, before sending anything, look at what is already loaded:

```text
/context
/env
```

`/context` shows how full the context window is and what is filling it. `/env` lists the instructions, MCP servers, skills and plugins that are loaded. All of that takes up room before your prompt arrives. Which of it does this task actually need?

---

## Stuck?

| Problem | Fix |
|---|---|
| Copilot Fusion is not in `/model`, or `--model fusion` is rejected | Run `/update`, `/exit` and start again. Still missing? Your plan or an admin policy excludes the models Fusion uses. Pair up with a neighbour. |
| No Claude Opus in your list | Normal: your organisation decides which models you see. Pick the strongest model you have and write its name down. |
| The start command is rejected | Start plain `copilot`, then `/limits set max-ai-credits 60` and pick the model with `/model`. |
| The run stops early at the 60-credit cap | That is the price gap making itself felt. Note it, run `/limits set max-ai-credits 120`, then type `continue`. |
| Copilot asks to run a command | Read-only ones (`ls`, `cat`, `grep`) are fine. Say no to anything that edits files or runs the app. |
| Something got edited anyway | `! git status --short` shows it, `! git checkout -- console` puts it back. The `!` runs it in your shell, so it costs nothing. |
| Fusion picked the same model as your Run A | Run B may reuse some of Run A's cache and look a little cheaper. Note it next to your result. |

---

## Takeaways

- **Fusion is a router, not a model.** You choose the effort level; Fusion chooses the model, says why, and `/usage` shows what it billed.
- **Most work doesn't need the Ferrari.** Reading and explaining code is everyday work, and everyday work is where routing saves the most.
- **Same prompt, same scope, two bills.** Measure before you make anything your default, Fusion included.
- **Cheaper only counts if the answer holds.** That is what the answer key is for.
- **A fresh session is the fair reset.** `/exit` and start again, so the meter shows one run only.
- **Effort is a dial.** Standard for everyday work. High and Max can use more than one model, so a task can cost more credits. Save them for problems that are genuinely hard.

Next: [Lab 1 · Size it, cap it, record it](1-size-limit-record.md) · Back to the [overview](../README.md)
