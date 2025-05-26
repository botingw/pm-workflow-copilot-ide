# pm-workflow-copilot-ide

![GitHub last commit](https://img.shields.io/github/last-commit/your‑org/pm‑workflow‑copilot‑ide)
![GitHub license](https://img.shields.io/github/license/your‑org/pm‑workflow‑copilot‑ide)
![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)

> **AI Product‑Management copilot for Cursor & Cline IDEs** ‑ guiding you from idea ➜ MVP docs with chat‑first workflows.

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

A typical chat might look like:

```
You: Users keep forgetting weather alerts. Idea: hyper‑local rain pings.
Copilot: Great! Let’s align strategically. Who benefits most, and what business goal does it serve?
```

---

## ⚡ Quick Start

```bash
# 1 – clone the repo (or copy rules file into an existing project)
$ git clone https://github.com/your‑org/pm‑workflow‑copilot‑ide.git

# 2 – point your IDE to the rules file
#    Cursor: no further works to do
#    Cline : no further works to do
#    Roo Code, Github Copilot, Windsurf, etc: copy .clinerules/.pm_workflow_assistant to specified paths for project/workspace custom rules in these IDEs 

# 3 – open a project folder and start chatting
```

> **Tip:** keep your product‑management artefacts in git.  They get versioned automatically, and reviewers can PR suggestions like any code change.

---

## 🛠️ Repository Layout

```
pm‑workflow‑copilot‑ide/
├── pm_rules.txt                   # Core prompt rules loaded by IDE
├── docs/
│   └── product_management_workflow_startup.md  # Detailed framework (read‑only)
├── examples/                      # End‑to‑end transcripts & sample artefacts
└── pm_project_docs/
    └── weather‑app/               # ← generated per project
        ├── opportunity_brief.md
        ├── mvp_scope.md
        ├── usability_findings.md
        ├── technical_feasibility.md
        ├── business_viability.md
        └── pm-progress.json
```

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

* Inspired by Tom Preston‑Werner’s *"README first"* philosophy.
* Workflow adapted from the open‑source \[Product Management Workflow for Startups].
* Badges by [shields.io](https://shields.io).
