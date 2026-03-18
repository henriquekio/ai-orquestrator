# Codex Orchestrator

This folder contains the Codex adaptation of the orchestrator generated from the `.claude` source tree.

## Structure

- `personas/` contains the Codex persona definitions.
- `rules/` contains the generated Codex rule definitions.
- `skills/` contains the generated Codex skill definitions.
- `AGENTS.md` at the repository root is the Codex entrypoint and points here.

## Operating Rules

- Start with `maestro`.
- Use the minimum number of personas needed to complete the request.
- Preserve explicit handoffs between personas.
- Do not let one persona perform another persona's specialist work.
- If context is missing, route to `contextualizer` before architecture or implementation decisions.
- If the request needs product discovery, requirement clarification, or a PRD, route to `product-manager`.
- If the request is architectural, route to `staff-engineer`.
- If the request is frontend implementation, route to `frontend-engineer`.
- If the request is frontend quality review, route to `frontend-reviewer`.

## Persona Index

- [personas/maestro.md](./personas/maestro.md)
- [personas/contextualizer.md](./personas/contextualizer.md)
- [personas/product-manager.md](./personas/product-manager.md)
- [personas/staff-engineer.md](./personas/staff-engineer.md)
- [personas/frontend-engineer.md](./personas/frontend-engineer.md)
- [personas/frontend-reviewer.md](./personas/frontend-reviewer.md)

## Rule Index

- [rules/README.md](./rules/README.md)
- [rules/mandatory/git.md](./rules/mandatory/git.md)
- [rules/mandatory/react.md](./rules/mandatory/react.md)
- [rules/mandatory/typescript.md](./rules/mandatory/typescript.md)
- [rules/recommended/react.md](./rules/recommended/react.md)
- [rules/recommended/typescript.md](./rules/recommended/typescript.md)
- [rules/optional/typescript.md](./rules/optional/typescript.md)

## Skill Index

- [skills/create-skill/SKILL.md](./skills/create-skill/SKILL.md)
- [skills/convert-orquestrator/SKILL.md](./skills/convert-orquestrator/SKILL.md)
