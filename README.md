# pm-workflow-copilot-ide

![GitHub last commit](https://img.shields.io/github/last-commit/your‑org/pm‑workflow‑copilot‑ide)
![GitHub license](https://img.shields.io/github/license/your‑org/pm‑workflow‑copilot‑ide)
![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)

> **AI Product‑Management copilot for Cursor & Cline IDEs** ‑ guiding you from idea ➜ MVP docs with chat‑first workflows.

---

## 💡 Example Ideas for Testing

This pack includes a `memory_starters/examples` directory containing several sample product ideas (e.g., `weather.md`, `to-do_list.md`).

To quickly test the product management workflow, you can start a conversation with your AI assistant about one of these ideas. For example, try saying:

> "Let's start working on a weather app."

The assistant will then guide you through the process, creating documents based on the workflow defined in this pack.

---

## 🚀 Why this project?

Product teams at fast‑moving startups rarely have time to open Confluence.  Yet skipping structured discovery & scoping leads to feature creep and re‑work.  **pm‑workflow‑copilot‑ide** embeds a lightweight, opinionated product‑management workflow *inside* the editor chat you already use, keeping momentum while safeguarding first‑principles rigor.

---

## 🧩 How it works

1. **Rules file** is loaded by Cursor/Cline so the assistant understands the workflow and file‑naming conventions.
2. On first mention of a project (e.g. “weather app”) the copilot creates `pm_project_docs/<project_name>/`.
3. For every workflow step it suggests the *next best action* and offers to auto‑generate artefacts (Opportunity Brief, MVP Scope, Usability Findings…).
4. All artefacts are Markdown stored alongside code, enabling *docs‑as‑code* review flows.
5. Progress is logged to `pm-progress.json` for instant context recall.

---
## 💬 What Using the Copilot Feels Like (Sample Dialogs)

Below are a handful of concise interactions that illustrate typical usage. Real wording varies by IDE, but the flow stays the same.

### 1. Kick‑off from a Rough Idea

```text
You: I want to build an app that helps freelancers track billable hours.
Copilot: Excellent! Let’s begin with Strategic Alignment. Who's the primary user and what pain are we solving?
```

### 2. Checking Project Progress

```text
You: How far along is my "weather_app" project and what's next?
Copilot: Progress → Product Charter ✓  •  User Flow ✓  •  MVP Scope ✓  
Next → Prototype & usability testing → `usability_findings.md` → business viability check.
```

### 3. Clarifying Workflow Stage

```text
You: Which phase are we in now?
Copilot: You're in Feasibility & Viability. Technical feasibility completed; business viability still pending. Shall I draft `business_viability.md`?
```

### 4. Requesting a New Artefact

```text
You: Generate the MVP scope for the budgeting tool, please.
Copilot: Drafting `pm_project_docs/budgeting_tool/mvp_scope.md` with user stories, success metrics, and out‑of‑scope items…
```

*(Conversation styles differ across IDEs; snippets are simplified for readability.)*

---

## 📦 Installation

This pack can be used with an AI-powered IDE in two ways: automatically with the `rulebook-ai` CLI, or by manually configuring your IDE.

### With Rulebook-AI (Recommended)

[Rulebook-AI](https://github.com/botingw/rulebook-ai) is a cross-IDE toolkit that manages AI assistant rules and memory.

1.  **Install the `rulebook-ai` CLI:**

    First, clone the Rulebook-AI repository and install it in editable mode using `uv`:
    ```bash
    git clone https://github.com/botingw/rulebook-ai.git
    cd rulebook-ai
    uv run pip install -e .
    cd ..
    ```

2.  **Add the Pack:**

    This repository contains the `pm-workflow-copilot` pack. From the root of the `pm-workflow-copilot-ide` project directory, or root of any repo you want install this pack, run the following command to add the pack:

    ```bash
    rulebook-ai packs add pm-workflow-copilot
    rulebook-ai project sync --pack pm-workflow-copilot
    ```

    The CLI will validate the pack and make it available to your IDE's AI assistant.

3.  **Start Chatting:**

    You're all set. Open a new chat and start with an idea, like `"Let's work on a weather app."`

> **Tip:** keep your product‑management artefacts in git.  They get versioned automatically, and reviewers can PR suggestions like any code change.

---
## 📦 Pack Layout

This pack has a specific structure that `rulebook-ai` recognizes. Here is an overview of the key directories and files within the `pm-workflow-copilot-pack` and what they do.

```
pm-workflow-copilot-pack/
├── manifest.yaml
├── README.md
├── memory_starters/
│   ├── docs/
│   │   ├── product_management_workflow_startup.md
│   │   └── pm-progress-template.json
│   └── examples/
│       └── ...
└── rules/
    └── 01-rules/
        └── 01-pm_workflow_assistant.md
```

### Key Components

*   `manifest.yaml`: This file contains metadata about the pack, such as its name (`pm-workflow-copilot`), version, and a brief summary. The `rulebook-ai` CLI uses this for identification.

*   `rules/`: This is the core of the pack. It contains the instructions that tell the AI assistant how to behave.
    *   `01-pm_workflow_assistant.md`: The main rule file. It defines the entire product management workflow, from strategic alignment to final requirements. It tells the assistant how to guide the user, what questions to ask, and which documents to generate.

*   `memory_starters/`: This directory contains documents that are loaded into the AI's short-term memory when the pack is activated. This gives the assistant the foundational knowledge it needs to operate.
    *   `docs/product_management_workflow_startup.md`: The detailed, formal specification of the product management workflow. The assistant consults this as its primary reference.
    *   `docs/pm-progress-template.json`: The JSON schema for the progress tracking file.
    *   `examples/`: Sample product ideas that you can use to test the pack's workflow.

### Generated Project Artifacts

When you use this pack in your own project, the assistant will generate a new directory at the root of your project folder:

*   `pm_project_docs/`: This folder is created automatically in your project's root directory the first time you start working on a new product idea with the assistant.
    *   `[project_name]/`: Inside `pm_project_docs`, a sub-directory is created for each product idea you work on (e.g., `weather_app/`).
    *   `*.md`: All the product management documents (Product Charter, PRD, etc.) are saved as Markdown files inside their respective project folder.
    *   `pm-progress.json`: A file that tracks your progress through the workflow for a specific project.

This structure keeps all your product documentation neatly organized alongside your code, right where you work.

---

## 📓 Workflow Cheatsheet

| Phase                   | Key Output                                            | Trigger Command / Prompt  |
| ----------------------- | ----------------------------------------------------- | ------------------------- |
| Strategic Alignment     | `product_charter.md`                                  | "Who is this for?"        |
| Problem Discovery       | `opportunity_brief.md`                                | "Draft 5 survey Qs"       |
| Solution Definition     | `mvp_scope.md`                                        | "Prioritize MVP features" |
| Feasibility & Viability | `technical_feasibility.md`<br>`business_viability.md` | "Assess tech risks"       |
| Requirements            | `prd.md`                                              | "Generate PRD"            |


---

## ⚠️ Experimental Status

> **Heads‑up:** *pm‑workflow‑copilot‑ide* began as a proving ground for bringing lightweight product‑management support into the broader **[Rulebook‑AI](https://github.com/botingw/rulebook-ai)** ecosystem — a cross‑IDE "rules + memory bank" toolkit for AI coding assistants. The long‑term plan is to merge this functionality upstream and deprecate this standalone repo once parity is reached. Follow the Rulebook‑AI repo for consolidated updates.

---

## 🗺️ Roadmap

* [ ] Context‑aware commands for VS Code extension
* [ ] Slack bot companion for cross‑functional reviews
* [ ] Automatic link‑back between PRs and related PM artefacts

Check the [issues list](https://github.com/your‑org/pm‑workflow‑copilot‑ide/issues) for more.

---

## 🤝 Contributing

1. **Fork** and create a feature branch.
2. Follow *Conventional Commits* for commit messages.
3. Run `pre‑commit install` to auto‑format Markdown.
4. Open a PR – the README’s badges will update once CI passes.

We love fresh perspectives from PMs, designers & engineers alike.

---

## 🔒 License

Distributed under the **MIT License**.  See `LICENSE` for details.

---

## 🙏 Acknowledgements

* Inspired by Tom Preston‑Werner’s *'''README first'''* philosophy.
* Workflow adapted from the open‑source \[Product Management Workflow for Startups].
* Badges by [shields.io](https://shields.io).# pm-workflow-copilot-ide

![GitHub last commit](https://img.shields.io/github/last-commit/your‑org/pm‑workflow‑copilot‑ide)
![GitHub license](https://img.shields.io/github/license/your‑org/pm‑workflow‑copilot‑ide)
![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)