# spec-development

## Purpose

This skill is used to turn a completed spec into a structured development plan that agents can read and execute. Use it after `create-spec` has produced a spec file and before any implementation begins. The output is a `plan.md` file placed alongside the spec, containing a feature brief, all technical decisions, and a fully broken-down task list that agents can follow step by step.

## Procedure

1. Ask the user for the path to the spec file (e.g. `specs/button/1.0.0/spec.md`). Read the file before doing anything else.

2. Evaluate the spec for completeness. A spec is ready for planning if it contains at minimum: an overview, requirements, and acceptance criteria. If the spec is missing critical sections, surface the gaps and stop — do not produce a plan from an incomplete spec.

3. Interview the user to collect the technical context needed to write a precise plan. The following areas must all be covered before writing:

   - **Architecture** — how the feature fits into the existing system (new component, new module, extends existing pattern, standalone, etc.)
   - **Constraints** — existing rules, patterns, or decisions that must be respected (project rules from `./rules/`, existing component patterns, monorepo structure, CI requirements, etc.)
   - **Libraries** — which libraries are available or required (component libraries, utility libraries, testing libraries, etc.). Note any that are prohibited.
   - **Performance** — any explicit performance requirements or considerations (bundle size, render frequency, memoization needs, lazy loading, etc.)
   - **Approach** — the implementation strategy (TDD, component-first, API-first, data-layer-first, etc.) and any architectural patterns to follow (compound components, render props, hooks-only, etc.)

   Ask only about what is not already answered by the spec. Group related gaps into a single round of questions. Do not ask for information that can be reasonably inferred from the spec and mandatory project rules.

4. Once all areas are covered, write the plan file to `specs/<feature-name>/<semver>/plan.md`, alongside the spec.

5. The plan file must contain all of the following sections in order:

   - **Feature Brief** — two to four sentences summarising what is being built, why, and what the plan covers. This is what an agent reads first to orient itself.

   - **Technical Context** — a structured summary of the decisions collected in step 3:
     - Architecture
     - Constraints
     - Libraries
     - Performance considerations
     - Approach

   - **Task List** — a sequenced list of tasks. Each task must be:
     - Small enough to implement and verify in a single focused session
     - Independently testable without requiring other incomplete tasks to be done first (except those listed as dependencies)
     - Written so an agent can read it and know exactly what to produce

   Each task must follow this structure:

   ```
   ### Task <N> — <title>

   **Description:** <what needs to be built and any relevant implementation notes>

   **Acceptance Criteria:**
   - <specific, verifiable condition>
   - <specific, verifiable condition>

   **Dependencies:** Task <N>, Task <N> — or "None" if this task has no prerequisites
   ```

## Guard rails

- Do not write the plan before reading the spec file — the spec is the source of truth for requirements and acceptance criteria.
- Do not produce a plan from an incomplete spec. Surface what is missing and stop.
- Do not invent architectural decisions, library choices, or constraints that were not confirmed by the user or derivable from the project rules.
- Do not produce tasks that are too large to implement and test in isolation — if a task feels large, break it down further.
- Do not produce tasks that duplicate the acceptance criteria from the spec verbatim — task-level criteria should be scoped to the task, not the full feature.
- Do not include implementation details that belong to the agent's discretion (exact variable names, file structure below the module level, etc.).
- Do not skip the Technical Context section — agents must have all decisions in one place before they start.
- Do not overwrite an existing plan at the same path without warning the user and confirming they want to replace it.
