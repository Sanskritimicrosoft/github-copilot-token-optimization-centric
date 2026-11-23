# Token optimisation with GitHub Copilot CLI

**Centric AI Agentic Factory Bootcamp · Iași · November 2026**

One task, two bills. Run the same coding task on one strong model and on **Copilot Fusion**, read the AI-credit meter after each run, and find out when routing saves money without costing quality.

| | |
|---|---|
| **Core lab** | 30 minutes: get set up, run the Fusion lab, share your result |
| **Stretch labs** | Five more labs for fast finishers, or to take home |
| **You need** | A GitHub account with a Copilot licence, plus Copilot CLI on your laptop or a browser for Codespaces |
| **Cost** | About 12–25 AI credits per person for the core lab (≈ $0.12–$0.25; 1 AI credit = $0.01) |

## Your 30 minutes

| Time | Step | Go to |
|---|---|---|
| 0–5 min | Get set up | [Lab 0](#lab-0--get-set-up-5-min) on this page |
| 5–25 min | Run the same task twice and compare the bills | [Fusion lab](lab/fusion-same-task.md) |
| 25–30 min | Discuss the room's results | Led by the presenters |
| Finished early? | Pick a stretch lab | [Stretch labs](#stretch-labs) |

## Before the session (10 min)

Install the tools beforehand so setup takes five minutes on the day. Can't install software on your laptop? Skip this and use [Codespaces](#option-b--github-codespaces-nothing-to-install) instead.

| Tool | Windows | macOS | Needed for |
|---|---|---|---|
| Copilot CLI | `winget install GitHub.Copilot` | `brew install --cask copilot-cli` | Everything |
| PowerShell 7 | `winget install --id Microsoft.PowerShell --source winget` | not needed | Copilot CLI on Windows (needs PowerShell 6 or later) |
| GitHub CLI (`gh`) | `winget install --id GitHub.cli` | `brew install gh` | Cloning in Lab 0, and the stretch labs |
| Node.js 22 or later | `winget install OpenJS.NodeJS.LTS` | `brew install node` | Stretch labs only |

---

## Lab 0 · Get set up (5 min)

**You're done when:** Copilot CLI is open in **your own copy** of this repo and `/usage` responds.

### 1 · Create your own copy of this repo

The stretch labs create issues, labels and comments, so everyone works in their own copy, not this one.

1. Sign in to github.com with the **GitHub account that has your Copilot licence for this bootcamp**. Whatever you create belongs to the account you're signed in with.
2. At the top of this page, click the green **Use this template** button, then **Create a new repository**.
3. Choose your account as the owner, give the repo a name and click **Create repository**.

No **Use this template** button, or your account is missing from the owner list? You're probably signed in with a different account. Switch accounts, or raise a hand.

Now open Copilot CLI in your copy. Pick one:

- **Copilot CLI installed on your laptop?** Go to [Option A](#option-a--copilot-cli-on-your-laptop).
- **Can't install it, or it won't start?** Go to [Option B](#option-b--github-codespaces-nothing-to-install).

### Option A · Copilot CLI on your laptop

Make sure the GitHub CLI is signed in with the same account:

```bash
gh auth status
```

It shows the wrong account, or none? Run `gh auth login` and sign in with the account from step 1.

Clone your copy and start Copilot CLI in it:

```bash
gh repo clone <your-github-username>/<your-repo-name>
cd <your-repo-name>
copilot
```

1. **Trust the folder** when Copilot CLI asks.
2. **Sign in** if it asks you to: type `/login` and use the account that has your Copilot licence.
3. **Update:** type `/update` so you're on the latest version.
4. **Check:** type `/usage`. If it responds, you're done.

Continue to the [Fusion lab](lab/fusion-same-task.md).

### Option B · GitHub Codespaces (nothing to install)

On the page of the repo you created in step 1: green **Code** button → **Codespaces** tab → **Create codespace on main**.

<img src="https://docs.github.com/assets/cb-49943/mw-1440/images/help/codespaces/who-will-pay.webp" alt="Code → Codespaces → Create codespace on main" width="25%">

Wait about two minutes for the container to build. Then, in the codespace terminal, install the latest Copilot CLI and start it:

```bash
curl -fsSL https://gh.io/copilot-install | sudo bash
copilot
```

The codespace already runs as your account, so there's nothing to sign in to. Type `/usage`. If it responds, you're done.

Continue to the [Fusion lab](lab/fusion-same-task.md).

---

## The labs

### Core lab

| Lab | What you'll do | Time |
|---|---|---|
| [Fusion lab · Same task, two bills](lab/fusion-same-task.md) | Give Copilot one read-only task on a strong model, then on Copilot Fusion. Score both answers and compare the AI credits. | 20 min |

### Stretch labs

For fast finishers, or to take home. Each one stands alone unless the table says otherwise.

| Lab | What you'll do | Time | Needs |
|---|---|---|---|
| [1 · Size it, cap it, record it](lab/1-size-limit-record.md) | Fix the bug you found in the Fusion lab inside a credit budget, and record what it cost on the issue | About 20 min | Node.js 22+, `gh` |
| [2 · See cache continuity](lab/2-keep-cache-warm.md) | Watch cached-input reuse change as you switch model and reasoning effort | 10 min | Nothing extra |
| [3 · Build a live cache clock](lab/3-build-cache-clock.md) | Have Copilot build a cache-expiry countdown against a test suite | 10 min | Lab 2, Node.js 22+ |
| [4 · Estimate from your own data](lab/4-estimate-from-history.md) | Size a new task from recorded actuals instead of a guess | About 15 min | Node.js 22+, `gh` |
| [5 · Ask your sessions where the money went](lab/5-chronicle-cost-tips.md) | Get cost tips drawn from your own session history | About 5 min, take-home | Nothing extra |

---

## What it costs

Copilot usage is billed in **AI credits** (1 AI credit = $0.01). What a run costs depends on the model and on how many tokens it reads and writes.

- **Core lab:** about 12–25 AI credits per person, depending on the model you choose for Run A.
- **Safety cap:** every run in the Fusion lab starts with `--max-ai-credits 60`, a soft cap on what each response may spend.
- **Promotion:** until 30 November 2026, paid Copilot plans get 30% off model costs when using Copilot Fusion.

## Need help?

- Every lab ends with a **Stuck?** section.
- During the bootcamp, raise a hand. Sanskriti and Sushil are in the room.

## About this repo

Every lab runs against the **Incident Console** in `console/`: a tiny, dependency-free terminal dashboard. Its metrics are simulated but deterministic, so everyone sees the same numbers.

Stretch labs 1–5 and the scripts, skills and plugin that support them come from Karol Muciek's [GitHub Copilot token optimization workshop](https://github.com/karolmckgh/github-copilot-token-optimization). This edition adds the Fusion lab, and is presented at the Centric AI Agentic Factory Bootcamp by Sanskriti Vagrecha and Sushil Kumar Jha.
