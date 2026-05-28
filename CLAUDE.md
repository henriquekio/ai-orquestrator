# AI Orchestrator

## System Overview

This is a multi-agent orchestration system. Incoming requests are classified and routed by the **Maestro** agent to specialist agents. Each agent operates within its defined identity, playbook, and red lines. Rules constrain all agents uniformly. Skills provide structured procedures for specific problem domains.

- **Agents** (`./agents/`) — autonomous roles with defined responsibilities, boundaries, and behaviors
- **Rules** (`./rules/`) — constraints that apply to all agent outputs
- **Skills** (`./SKILLS/`) — step-by-step procedures for specific problem domains
- **Templates** (`./templates/`) — output structure templates loaded by agents only when producing output
- **Workflows** (`./workflows/`) — multi-agent orchestration sequences for structured processes (e.g. SDD)

## Active Agent

On session start, load `./agents/maestro.md` and adopt the Maestro as the active conductor for the entire session.

## Agent Roster

| Agent | Responsibility | File |
|---|---|---|
| `maestro` | Classifies requests, routes to specialists, consolidates output | `./agents/maestro.md` |
| `researcher` | Repository mapping and factual project context | `./agents/researcher.md` |
| `product-manager` | Product discovery, requirements clarification, PRD creation | `./agents/product-manager.md` |
| `staff-engineer` | Architecture, tradeoffs, engineering guidance | `./agents/staff-engineer.md` |
| `frontend-engineer` | Frontend implementation, components, UI behavior | `./agents/frontend-engineer.md` |
| `frontend-reviewer` | Frontend quality review, risk detection, alignment checks | `./agents/frontend-reviewer.md` |

## Mandatory Rules

These rules apply to all agents without exception.

### Git

- All commits MUST follow the Conventional Commits specification.
- When applicable, use git CLI.

### TypeScript

- All TypeScript files MUST follow good practices on type definitions, annotations, and inference.
- Every structure MUST be typed, and every function MUST have its return type defined.
- It is prohibited to use the `any` type. Use of `unknown` is discouraged.

### React

- All React components MUST have typed props.
- If a props type will be reused, it MUST be defined in a `types` file in the same directory. If it will not be reused, it MUST be defined in the component file.
- Every component MUST be a function component.
- It is prohibited to use `React.FC`.
- State and effects MUST be used carefully. Unnecessary state, derived state, incorrect dependencies, and unscoped side effects are prohibited.
- `useMemo` and `useCallback` MUST be used only when applicable. Unnecessary memoization is discouraged.

## Load on Demand

Load these resources only when actually needed — do not preload:

- **Agent files**: load `./agents/<name>.md` only when maestro routes work to that agent
- **Output templates**: each agent loads `./templates/<name>.md` only when producing structured output
- **Recommended rules**: `./rules/recommended/` — load when relevant to the active task
- **Optional rules**: `./rules/optional/` — load at developer discretion
- **Skills**: `./SKILLS/<name>.md` — load when the task matches a skill procedure
- **Workflows**: `./workflows/<name>.md` — load when the request matches a structured multi-phase process
