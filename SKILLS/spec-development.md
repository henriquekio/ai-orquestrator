# spec-development

## Purpose

Use this skill to turn a completed spec into a structured development plan that agents can read and execute without ambiguity. It bridges the gap between "what we are building" (the spec) and "how we will build it" (a sequenced, technical task list). Use it after `create-spec` and before any implementation begins.

A good plan prevents agents from making architectural guesses mid-implementation and prevents work from landing in the wrong order or being untestable in isolation.

## Procedure

1. Ask the user for the path to the spec file (e.g. `specs/button/1.0.0/spec.md`). Read the file before doing anything else — the spec is the source of truth. Do not rely on the conversation summary of the spec; read the actual file.

2. Check whether the spec is ready for planning. A spec is plannable if it contains at minimum: an overview, requirements, and acceptance criteria. If critical sections are missing, tell the user what is missing and why it blocks planning — an incomplete spec produces a plan with gaps that surface as blockers during implementation.

3. Collect the technical context needed to make the plan precise. The five areas below must all be covered. Ask only about what is not already answered by the spec or inferable from the project's mandatory rules. Group related questions into a single round rather than asking one at a time — this interview should feel efficient, not exhausting.

   - **Architecture** — where does this fit in the existing system? (new module, new component, extension of an existing pattern, standalone)
   - **Constraints** — what must be respected? (project rules in `./rules/`, existing component patterns, monorepo boundaries, CI requirements)
   - **Libraries** — what is available or required? What is prohibited?
   - **Performance** — any explicit performance budget or concerns? (bundle size, render frequency, memoization needs)
   - **Approach** — what implementation strategy? (TDD, component-first, API-first) What patterns must be followed?

4. Write the plan file to `specs/<feature-name>/<semver>/plan.md`, alongside the spec. Warn the user if a plan already exists at that path before overwriting.

5. The plan must contain all of the following sections in order:

   **Feature Brief** — two to four sentences: what is being built, why it matters, and what the plan covers. This is the first thing an agent reads to orient itself before looking at any task.

   **Technical Context** — a structured summary of everything collected in step 3. Agents must have all technical decisions in one place. Do not scatter them across task descriptions.

   ```
   - Architecture: <how this fits the system>
   - Constraints: <rules and patterns to respect>
   - Libraries: <what to use / what to avoid>
   - Performance: <budget or considerations>
   - Approach: <strategy and patterns>
   ```

   **Task List** — a sequenced list of tasks. Good tasks share three properties: they are small enough to implement and verify in a single focused session, they are testable without relying on incomplete sibling tasks (except explicit dependencies), and they are written precisely enough that an agent knows exactly what to produce.

   A useful sizing heuristic: if a task involves more than one distinct concern (e.g. "build the component AND write the tests AND wire up the state"), split it. Each task should have one clear deliverable.

   Each task uses this format:

   ```
   ### Task <N> — <title>

   **Description:** <what needs to be built and any relevant implementation notes>

   **Acceptance Criteria:**
   - <specific, verifiable condition>
   - <specific, verifiable condition>

   **Dependencies:** Task <N>, Task <N> — or "None"
   ```

   **Example of a well-sized task:**
   ```
   ### Task 1 — Define Button prop types

   **Description:** Create the TypeScript interface for the Button component props. Include all native HTML button props via `React.ComponentPropsWithoutRef<"button">`, plus `isLoading: boolean`, `icon?: ReactNode`, and `iconAlignment?: "left" | "right"`.

   **Acceptance Criteria:**
   - The props interface compiles without error
   - `isLoading`, `icon`, and `iconAlignment` are explicitly typed
   - Native HTML button props are inherited, not manually duplicated

   **Dependencies:** None
   ```

## Guard rails

The plan is derived from the spec — read the file, not your memory of the conversation. If you plan from a summary you risk missing constraints or acceptance criteria that an agent will later need to satisfy.

Task-level acceptance criteria should be scoped to the task, not copied verbatim from the spec. The spec defines feature-level behavior; task criteria verify that the specific deliverable of that task is correct. Duplicating spec criteria at the task level creates confusion about scope and inflates the apparent done-ness of a task.

Do not invent architectural decisions or library choices that were not confirmed. Agents treat the Technical Context section as settled fact — unconfirmed decisions made here will propagate into the implementation and be hard to reverse.

Implementation details that belong to the agent's discretion (exact variable names, internal file structure, comment style) should not appear in the plan. The plan defines what to build and how to verify it; the agent decides how to structure the code within those boundaries.
