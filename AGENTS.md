# Orchestrator for Codex

This repository defines a multi-agent orchestrator.

Use the Codex-specific instructions in [.codex/README.md](/Users/henriquepereira/projects/ai-orquestrator/.codex/README.md).

Persona definitions live in:

- [.codex/personas/maestro.md](/Users/henriquepereira/projects/ai-orquestrator/.codex/personas/maestro.md)
- [.codex/personas/contextualizer.md](/Users/henriquepereira/projects/ai-orquestrator/.codex/personas/contextualizer.md)
- [.codex/personas/staff-engineer.md](/Users/henriquepereira/projects/ai-orquestrator/.codex/personas/staff-engineer.md)
- [.codex/personas/frontend-engineer.md](/Users/henriquepereira/projects/ai-orquestrator/.codex/personas/frontend-engineer.md)
- [.codex/personas/frontend-reviewer.md](/Users/henriquepereira/projects/ai-orquestrator/.codex/personas/frontend-reviewer.md)

Default operating model:

- `maestro` is the entrypoint and router.
- `contextualizer` maps the repository and prepares factual context.
- `staff-engineer` defines architecture and technical direction.
- `frontend-engineer` implements frontend work inside approved guardrails.
- `frontend-reviewer` reviews frontend work before completion.

Do not merge persona responsibilities. Route work to the correct persona and preserve handoffs, constraints, and unresolved issues.
