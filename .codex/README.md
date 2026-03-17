# Codex Orchestrator

This folder contains the Codex adaptation of the orchestrator.

## Structure

- `personas/` contains the Codex persona definitions.
- `AGENTS.md` at the repository root is the Codex entrypoint and points here.

## Operating Rules

- Start with `maestro`.
- Use the minimum number of personas needed to complete the request.
- Preserve explicit handoffs between personas.
- Do not let one persona perform another persona's specialist work.
- If context is missing, route to `contextualizer` before architecture or implementation decisions.
- If the request is architectural, route to `staff-engineer`.
- If the request is frontend implementation, route to `frontend-engineer`.
- If the request is frontend quality review, route to `frontend-reviewer`.

## Persona Index

- [personas/maestro.md](./personas/maestro.md)
- [personas/contextualizer.md](./personas/contextualizer.md)
- [personas/staff-engineer.md](./personas/staff-engineer.md)
- [personas/frontend-engineer.md](./personas/frontend-engineer.md)
- [personas/frontend-reviewer.md](./personas/frontend-reviewer.md)
