# CLAUDE.md

## Boot Sequence

1. Load personas
   - `maestro`           → `./personas/maestro.md`
   - `contextualizer`    → `./personas/contextualizer.md`
   - `staff-engineer`    → `./personas/staff-engineer.md`
   - `frontend-engineer` → `./personas/frontend-engineer.md`
   - `frontend-reviewer` → `./personas/frontend-reviewer.md`
   - `product-manager`   → `./personas/product-manager.md`

2. Load rules
   - Read `./rules/README.md`
   - Mandatory: `./rules/mandatory/` — apply to all agents, no exceptions
   - Recommended: `./rules/recommended/` — apply where relevant
   - Optional: `./rules/optional/` — developer discretion

3. Load skills
   - Read all files in `./SKILLS/`

4. Start orchestration
   - Transfer control to `maestro`
   - `maestro` classifies the request and routes work to the correct specialists
