# Workflow: Spec Driven Development (SDD)

## Purpose

This workflow enforces a structured, spec-first development process for any new feature or component. It ensures that intent is captured before architecture, architecture is captured before implementation, and every piece of work is reviewed before the next one begins. The user controls the two critical gates: spec approval and per-task review decisions.

## Trigger

Maestro should activate this workflow when the user's request signals intent to build something new — a feature, a component, a flow, or any user-facing capability. Recognition signals include:

- "I want to build / create / add..."
- "We need a [feature / component / page / flow]..."
- "Implement X for..."
- A product or engineering brief describing new functionality

When in doubt, classify as SDD rather than ad-hoc implementation. The cost of a spec is low; the cost of building the wrong thing is not.

---

## Phases

### Phase 1 — Specification

**Goal:** produce a user-approved spec before any architecture or implementation begins.

1. Load `./agents/researcher.md`. Ask the researcher to map the relevant parts of the repository — existing components, patterns, and conventions that the new feature must be consistent with. The researcher's output will be passed as context to the spec.

2. Load `./SKILLS/create-spec.md`. Run the `create-spec` skill with the user's request and the researcher's context as inputs. The skill will interview the user if the context is insufficient. The output is `specs/<feature-name>/<semver>/spec.md`.

3. Present the spec to the user. Ask explicitly: **"Does this spec reflect what you want to build? Approve to continue, or share what needs to change."**
   - **Approved** → proceed to Phase 2.
   - **Changes requested** → return to step 2 with the user's feedback. Revise and re-present. Do not proceed until the user approves.

---

### Phase 2 — Planning

**Goal:** produce a development plan with a sequenced task list before any code is written.

4. Load `./agents/staff-engineer.md`. Hand off the approved spec path (`specs/<feature-name>/<semver>/spec.md`). The staff engineer's responsibility in this phase is to:
   - Read the spec
   - Evaluate and collect technical context (architecture, constraints, libraries, performance, approach) — interviewing the user for anything unclear
   - Load `./SKILLS/spec-development.md` and run the `spec-development` skill to produce `specs/<feature-name>/<semver>/plan.md`

5. Once the plan is written, Maestro presents it to the user. Ask explicitly: **"Does this development plan look right? Approve to begin implementation, or share what needs to change."**
   - **Approved** → Maestro reads the plan to extract the full task list. The tasks are the unit of work for Phase 3. Do not begin implementation until the user has approved and the task list is known.
   - **Changes requested** → return to step 4 with the user's feedback. Staff engineer revises the plan and Maestro re-presents. Do not proceed until the user approves.

---

### Phase 3 — Implementation

**Goal:** implement each task in order, with a review gate after every task before proceeding.

For each task in the plan (from Task 1 to Task N), run the following loop:

6. Load `./agents/frontend-engineer.md`. Assign the task with:
   - the task description, acceptance criteria, and dependencies from the plan
   - the spec path for behavioral reference
   - the technical context from the plan's Technical Context section

7. Frontend engineer implements the task and returns the output to Maestro.

8. Load `./agents/frontend-reviewer.md`. Ask the reviewer to inspect the task output against:
   - the task's acceptance criteria
   - the spec's acceptance criteria for any related user stories
   - the project's mandatory rules

   **The reviewer must not present findings directly to the user.** The reviewer returns findings to Maestro only.

9. Maestro evaluates the reviewer's findings:
   - **No issues found** → mark the task complete and advance automatically. If more tasks remain, return to step 6 for the next task. If all tasks are complete, proceed to Phase 4. Do not interrupt the user.
   - **Issues found** → Maestro presents the findings to the user and asks: **"Send this task back to be fixed, or approve and continue anyway?"**
     - **Send back to fix** → load `./agents/frontend-engineer.md` and pass the reviewer's findings as the fix brief. After the engineer addresses the findings, return to step 8. The reviewer must re-review before the task can advance.
     - **Approve and continue** → mark the task complete and proceed to the next task.

---

### Phase 4 — Test Summary

**Goal:** give the user a clear, actionable test guide to verify the completed feature end to end.

10. Load `./agents/staff-engineer.md`. Ask the staff engineer to read the spec and the plan and produce a human-readable test summary. The summary must cover:
    - A brief description of what was built
    - For each user story in the spec: a plain-language description of how to verify it manually, derived from the GIVEN/WHEN/THEN acceptance criteria
    - Any edge cases or error paths that require explicit verification

11. Maestro presents the test summary to the user. The workflow is complete.

---

## Guardrails

- Never skip Phase 1 or begin Phase 2 before the user has explicitly approved the spec. A spec approved by Maestro alone is not approved.
- Never skip Phase 2 or begin Phase 3 before the user has explicitly approved the plan. A plan approved by Maestro alone is not approved. Improvised implementation without an approved plan breaks the SDD contract.
- Never allow the reviewer to address the user directly in Phase 3. All review communication goes through Maestro so the user receives a consistent, consolidated decision point.
- Only interrupt the user in Phase 3 when the reviewer found issues. Clean reviews advance automatically — unnecessary interruptions break the flow.
- Never proceed past a fix loop without a re-review. A fix that was not reviewed is not done.
- If the user abandons the workflow mid-way (asks for something unrelated), pause and confirm whether to resume or abandon SDD before acting on the new request.
