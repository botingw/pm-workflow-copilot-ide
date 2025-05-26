## MVP Design: Product Management Workflow Assistant for Cursor

This high-level design outlines a Minimum Viable Product (MVP) for a **Product Management Workflow Assistant** integrated into Cursor, using the provided `product_management_workflow_startup.md` as the workflow definition. The assistant enables non-professional users to navigate the pre-coding product management process (Strategic Alignment, Problem Discovery, Solution Definition, Feasibility & Viability, and Requirements) via natural language, offering step-by-step guidance and automating tasks like writing a PRD. The design leverages Cursor’s AI capabilities and custom rules to simplify the process, ensuring accessibility for users unfamiliar with product management.

---

### Core Assumptions
- **Workflow Document**: `docs/product_management_workflow_startup.md` defines five phases (Strategic Alignment & Foundation, Problem Discovery & Opportunity Validation, Solution Definition & MVP Shaping, Feasibility & Viability Checks, Finalizing Requirements & Engineering Handoff) with specific steps, actions, formal outputs (e.g., `product_charter.md`, `opportunity_brief.md`, `prd.md`), and Gemini Advice for flexibility.
- **Platform**: Cursor, an AI-powered IDE, supports custom rules, natural language interaction, and file generation.
- **User Needs**: Non-experts require intuitive guidance, reminders for next steps, and automated document creation, with the AI adapting to the user’s input and project state.

---

### MVP Feature Set
The MVP focuses on delivering a streamlined assistant within Cursor that guides users through the workflow in `product_management_workflow_startup.md`, emphasizing simplicity, natural language interaction, and automation for non-professionals.

1. **Natural Language Interface**
   - Users interact via Cursor’s chat panel, using plain language (e.g., “I want an app to help people track habits”).
   - The AI responds conversationally, avoiding jargon (e.g., “Let’s define what this app is about. Who needs it, and why?”).

2. **Workflow Parser**
   - Reads `docs/product_management_workflow_startup.md` to extract phases, steps, actions, outputs, and guidelines.
   - Maps the workflow into a structured format (e.g., JSON internally) to track tasks and outputs like `product_charter.md`, `opportunity_brief.md`, `mvp_scope.md`, `usability_findings.md`, `technical_feasibility.md`, `business_viability.md`, and `prd.md`.
   - Example internal mapping:
     ```json
     [
       {
         "phase": "Strategic Alignment",
         "steps": [
           {
             "name": "Define Guiding Principles",
             "output": "product_charter.md",
             "guidelines": "Contains mission, vision, North Star metric, target user summary, operating principles"
           }
         ]
       },
       ...
     ]
     ```

3. **Step Guidance and Task Automation**
   - **Guidance**: Suggests the next step based on the workflow and project state (e.g., “You’ve shared an idea. Next, let’s create a Product Charter to define the mission and target users.”).
   - **Automation**: Offers to generate documents (e.g., “I can draft a `product_charter.md` for you—want me to?”) or provide templates (e.g., user story format).
   - **Research Support**: Suggests lightweight research actions (e.g., “I can draft survey questions for user interviews or summarize online discussions about habit-tracking pain points.”).
   - **Flexibility**: Incorporates Gemini Advice by offering lean options (e.g., “For a quick start, we can make a shorter Product Charter. Want to keep it to one page?”).

4. **Context Tracking**
   - Maintains project state in `docs/pm-progress.json`, tracking completed phases, steps, and generated files (e.g., `{"current_phase": "Problem Discovery", "files": ["product_charter.md"]}`).
   - Ensures suggestions align with prior inputs and workflow requirements.

5. **Document Generation**
   - Creates workflow-specified outputs (e.g., `opportunity_brief.md`, `prd.md`) using templates derived from the workflow’s guidelines.
   - Example: For `prd.md`, synthesizes content from earlier files and user inputs, following the structure in the workflow (Introduction, MVP Scope, User Stories, etc.).

---

### Cursor Rules for the MVP
The assistant’s behavior is defined in Cursor’s `.cursorrules` file, tailored to the workflow in `product_management_workflow_startup.md`. These rules ensure the AI provides context-aware guidance and automation.

---

### Example User Interaction
1. **User**: “I want to build an app to help people track daily habits.”
2. **AI** (parsing `product_management_workflow_startup.md`): “Awesome! Let’s start with Strategic Alignment by creating a Product Charter. Can you tell me who this app is for and what the main goal is? For example, is it to make habits easier to stick to?”
3. **User**: “For busy professionals to stick to habits like exercising, because they forget.”
4. **AI**: “Got it. I can draft a `product_charter.md` with the mission, target users (busy professionals), and a North Star metric like ‘daily habit completions.’ Want me to create it now?”
5. **User**: “Yes, draft it.”
6. **AI**: (Generates `product_charter.md`: “Mission: Help busy professionals stick to daily habits. Target Users: Professionals aged 25-45. North Star: Daily habit completions.” Updates `pm-progress.json`.) “Done! Next, we’re in Problem Discovery. Should I draft survey questions to learn more about their pain points, or do you have some user feedback already?”
7. **User**: “Write a PRD.”
8. **AI**: “We need to complete Problem Discovery and Solution Definition first to make a solid PRD. Let’s create an `opportunity_brief.md` to clarify the problem and users’ needs. I can draft it based on what you’ve shared—okay?”

---

### Technical Implementation Notes
- **Platform**: Cursor’s AI (e.g., Grok integration) handles natural language processing and file generation.
- **Rules Setup**: Users place `.cursorrules` in the project root, and `docs/product_management_workflow_startup.md` is assumed to exist (or provided as a default template).
- **File Management**: Outputs are saved in `docs/` (e.g., `docs/product_charter.md`, `docs/prd.md`), and progress is tracked in `docs/pm-progress.json`.
- **MVP Scope**: Focuses on pre-coding phases (excludes development and testing, handled by Cursor’s existing features).
- **Templates**: The AI uses predefined templates for outputs (e.g., PRD structure from the workflow) but customizes content based on user inputs and prior files.
- **Extensibility**: Future versions could integrate web search for Problem Discovery or prototyping tools for Solution Definition.

---

### Why This MVP Works
- **Accessibility**: Natural language and proactive suggestions make the process approachable for non-experts.
- **Workflow-Driven**: Parsing `product_management_workflow_startup.md` ensures alignment with the defined process.
- **Automation**: Generating documents like `prd.md` saves time and reduces complexity.
- **Flexibility**: Gemini Advice integration allows lean options (e.g., shorter documents) for faster iteration.
- **Context-Aware**: Progress tracking ensures relevant guidance at each step.

---

### Next Steps for Development
1. Implement the workflow parser to extract phases, steps, and outputs from `docs/product_management_workflow_startup.md`.
2. Add the `.cursorrules` file to enable AI guidance and automation.
3. Create a `pm-progress.json` tracker for project state.
4. Test with sample inputs (e.g., “habit tracker app”) to verify guidance and document generation.

This MVP delivers a functional assistant that simplifies product management in Cursor, using the provided workflow to guide users and automate key tasks. Let me know if you’d like to refine the rules, add specific document templates, or explore further details!