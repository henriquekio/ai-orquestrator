# Orchestrator for Codex

This repository defines a multi-agent orchestrator.

Use the Codex-specific instructions in [.codex/README.md](.codex/README.md).

Persona definitions live in:

- [.codex/personas/maestro.md](.codex/personas/maestro.md)
- [.codex/personas/contextualizer.md](.codex/personas/contextualizer.md)
- [.codex/personas/product-manager.md](.codex/personas/product-manager.md)
- [.codex/personas/staff-engineer.md](.codex/personas/staff-engineer.md)
- [.codex/personas/frontend-engineer.md](.codex/personas/frontend-engineer.md)
- [.codex/personas/frontend-reviewer.md](.codex/personas/frontend-reviewer.md)

Generated rule definitions live in:

- [.codex/rules/README.md](.codex/rules/README.md)
- [.codex/rules/mandatory/git.md](.codex/rules/mandatory/git.md)
- [.codex/rules/mandatory/react.md](.codex/rules/mandatory/react.md)
- [.codex/rules/mandatory/typescript.md](.codex/rules/mandatory/typescript.md)
- [.codex/rules/recommended/react.md](.codex/rules/recommended/react.md)
- [.codex/rules/recommended/typescript.md](.codex/rules/recommended/typescript.md)
- [.codex/rules/optional/typescript.md](.codex/rules/optional/typescript.md)

Generated skill definitions live in:

- [.codex/skills/create-skill/SKILL.md](.codex/skills/create-skill/SKILL.md)
- [.codex/skills/convert-orquestrator/SKILL.md](.codex/skills/convert-orquestrator/SKILL.md)

Default operating model:

- `maestro` is the entrypoint and router.
- `contextualizer` maps the repository and prepares factual context.
- `product-manager` drives product discovery, requirement clarification, scope definition, and PRD creation.
- `staff-engineer` defines architecture and technical direction.
- `frontend-engineer` implements frontend work inside approved guardrails.
- `frontend-reviewer` reviews frontend work before completion.

Do not merge persona responsibilities. Route work to the correct persona and preserve handoffs, constraints, and unresolved issues.
