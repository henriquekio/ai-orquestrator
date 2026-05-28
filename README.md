# AI Orchestrator

A multi-agent orchestration system for Claude Code. It defines a team of specialist AI agents, the rules they follow, the skills they can execute, and the workflows that coordinate them — so that Claude behaves as a structured engineering team rather than a single generalist assistant.

The system is designed to be dropped into any project. Claude loads it automatically via `CLAUDE.md` and routes every request through a conductor agent (Maestro) that classifies work and delegates to the right specialist.

---

## How it works

The system is built from four types of resources:

**Agents** — autonomous roles with defined responsibilities, boundaries, and red lines. Each agent is loaded on demand when Maestro routes work to it.

| Agent | Role |
|---|---|
| `maestro` | Conductor. Classifies every request and routes it to the right specialist. Always active. |
| `researcher` | Maps the repository and produces factual context files for other agents. |
| `product-manager` | Drives product discovery, clarifies requirements, and produces PRDs. |
| `staff-engineer` | Defines architecture, evaluates tradeoffs, and produces implementation-ready direction. |
| `frontend-engineer` | Implements user-facing features within approved architecture and requirements. |
| `frontend-reviewer` | Reviews frontend work for correctness, accessibility, and alignment before it is accepted. |

**Rules** — constraints that apply to all agent outputs without exception. Mandatory rules (TypeScript, React, Git) are always in context. Recommended and optional rules are loaded when relevant.

**Skills** — step-by-step procedures agents follow for specific problem domains: `create-spec`, `spec-development`, `benchmark`.

**Workflows** — multi-phase orchestration sequences for structured processes. The built-in workflow is **SDD (Spec Driven Development)**.

---

## Setup

### Option A — Clone into your project

```bash
git clone https://github.com/henriquekio/ai-orquestrator .orchestrator
echo ".orchestrator/" >> .gitignore
```

Then add to your project's `CLAUDE.md`:

```md
## Orchestration System

Load the orchestration system from `./.orchestrator/CLAUDE.md`.
Resolve all agent and template paths relative to `./.orchestrator/`.
```

### Option B — Git submodule

```bash
git submodule add https://github.com/henriquekio/ai-orquestrator .orchestrator
```

Same `CLAUDE.md` instruction as above. The submodule approach keeps the orchestrator versioned with your project.

### How Claude loads it

When Claude Code starts a session in your project, it reads your `CLAUDE.md`, which instructs it to load `.orchestrator/CLAUDE.md`. That file bootstraps the system: it loads the Maestro agent and inlines the mandatory rules. All other agents, skills, and workflows are loaded on demand — only when actually needed — so the initial prompt stays lean.

---

## Using the SDD workflow

Spec Driven Development (SDD) is the default workflow for building new features. Maestro activates it automatically when it detects that you want to build something new.

### Start

Just describe what you want to build in plain language:

```
I want to build a reusable Button component with loading and icon support.
```

Maestro recognises the intent and starts the SDD workflow.

### Phase 1 — Specification

Maestro calls the **Researcher** to map relevant parts of the repository (existing components, patterns, conventions). Then it runs the `create-spec` skill, which interviews you if your description is missing any of five key areas:

- Who will use this?
- What problem does it solve?
- How will they interact with it?
- What outcomes matter?
- What is explicitly out of scope?

The output is a versioned spec file at `specs/<feature-name>/<version>/spec.md` containing an overview, requirements, out-of-scope items, user stories, acceptance criteria, and Mermaid flow diagrams.

**Maestro presents the spec and waits for your approval before continuing.**

### Phase 2 — Planning

Maestro hands the approved spec to the **Staff Engineer**, who collects technical context (architecture, constraints, libraries, performance, approach) — asking you about anything unclear — and runs the `spec-development` skill.

The output is a development plan at `specs/<feature-name>/<version>/plan.md` with a feature brief, a Technical Context section, and a sequenced task list. Each task has a description, acceptance criteria, and dependencies.

**Maestro presents the plan and waits for your approval before implementation begins.**

### Phase 3 — Implementation

Maestro works through the task list one task at a time:

1. **Frontend Engineer** implements the task.
2. **Frontend Reviewer** inspects it against the task's acceptance criteria and the spec.
3. If the review is clean → task is marked done and the next task starts automatically.
4. If the review finds issues → Maestro surfaces the findings and asks you: fix it or approve and continue.
   - **Fix** → Frontend Engineer addresses the findings, Reviewer re-reviews.
   - **Approve** → task is marked done and the next task starts.

### Phase 4 — Test summary

Once all tasks are complete, the **Staff Engineer** produces a human-readable test guide derived from the spec's acceptance criteria. Maestro presents it so you can verify the feature end to end.

---

## Project structure

```
agents/         Specialist agent definitions
rules/
  mandatory/    Always-applied rules (TypeScript, React, Git)
  recommended/  Applied when relevant
  optional/     Applied at developer discretion
SKILLS/         Skill procedure files (create-spec, spec-development, benchmark)
templates/      Output templates loaded by agents when producing structured output
workflows/      Multi-phase orchestration sequences (sdd.md)
CLAUDE.md       System entry point — loaded automatically by Claude Code
```
