# Workflow: Proposal Estimation

## Purpose

This workflow produces a structured effort estimate for a software project. It ensures the `proposal-estimator` has the right context before asking questions, that technical unknowns are resolved through the right specialists, and that all open questions are answered before the final estimate is produced.

## Trigger

Maestro should activate this workflow when the user's request signals intent to estimate effort, produce a proposal, or scope a project for a client-facing deliverable. Recognition signals include:

- "I need an estimate for..."
- "How long would it take to build..."
- "Prepare a proposal for..."
- "How many hours to..."
- A requirements document, PRD, or feature brief without an associated estimate

---

## Phases

### Phase 1 — Intake

**Goal:** give the `proposal-estimator` all available context before any analysis begins.

1. Load `./agents/proposal-estimator.md`.

2. Pass all available context to `proposal-estimator`:
   - The user's request
   - Any attached PRD, requirements document, or feature brief
   - Any prior technical context already established in the session

3. `proposal-estimator` reads the input and produces:
   - A plain-language summary of the solution as understood
   - A list of technical unknowns that require codebase or system context (if any)
   - A list of business or requirement questions for the user (if any)

   If neither list has entries, skip to Phase 4.

---

### Phase 2 — Technical Research (Conditional)

**Goal:** resolve technical unknowns through specialist agents before questioning the user.

Activate this phase only if `proposal-estimator` produced a list of technical unknowns in Phase 1.

4. Load `./agents/researcher.md`. Ask the researcher to map the parts of the repository relevant to the technical unknowns identified by `proposal-estimator`. The researcher returns findings to maestro — not to the user.

5. Load `./agents/staff-engineer.md`. Hand off:
   - The researcher's findings
   - The technical questions from `proposal-estimator`

   `staff-engineer` answers the technical questions and returns answers to maestro — not to the user.

6. Pass the researcher's findings and `staff-engineer`'s answers to `proposal-estimator`. `proposal-estimator` absorbs the context and updates its understanding.

7. `proposal-estimator` re-evaluates its question lists. If new technical unknowns emerged from the research answers, return to step 4. Otherwise proceed.

---

### Phase 3 — Interview Loop

**Goal:** resolve all remaining business and requirement questions before producing any number.

8. `proposal-estimator` groups remaining questions by theme and presents them to the user in a single batched message. Never ask one question at a time.

9. The user answers.

10. `proposal-estimator` evaluates: would any further question materially change a work package, the contingency level, or the final ranges?
    - **Yes** → prepare the next batch and return to step 8.
    - **No** → document any remaining unknowns as explicit assumptions and proceed to Phase 4.

---

### Phase 4 — Estimate Production

**Goal:** produce the final estimate document with no hidden assumptions or silent numbers.

11. `proposal-estimator` loads `./templates/proposal-estimator-estimate.md` and produces the internal estimate.

12. Load `./SKILLS/format-proposal.md`. Run the `format-proposal` skill using the internal estimate as input to produce the client-facing proposal document at `proposals/<project-name>.md`.

13. Maestro presents the client-facing document to the user. The workflow is complete.

---

## Guardrails

- Never skip Phase 3 or produce the estimate while resolvable questions remain open.
- Never allow `researcher` or `staff-engineer` to address the user directly in this workflow. All specialist output flows through maestro back to `proposal-estimator`.
- Never ask the user one question at a time. Questions must be batched by theme.
- Never bake contingency silently — it must appear as a visible line in the output.
- Never present a single hour number without best case, expected case, and worst case.
- Phase 2 is conditional — only activate it when `proposal-estimator` explicitly identifies technical unknowns that require codebase or system context.
- If the user abandons the workflow mid-way (asks for something unrelated), pause and confirm whether to resume or abandon before acting on the new request.
