# create-spec

## Purpose

This skill is used to produce a structured specification file following the Spec Driven Development (SDD) pattern. Use it before any implementation begins, whenever a new feature, flow, or product change needs to be clearly defined. The output is a versioned spec file that gives the entire team — product, design, and engineering — a shared and unambiguous definition of what is being built and why.

## Procedure

1. Read the context provided by the user. Evaluate whether it answers all four essential questions:
   - **Who** will use this? (user type, role, context)
   - **What problem** does it solve for them? (pain point, current friction, unmet need)
   - **How** will they interact with it? (entry points, flow, key actions, edge cases)
   - **What outcomes matter?** (success criteria, measurable goals, non-goals)

2. If any of the four questions is unanswered or too vague to produce a precise spec, interview the user before writing anything. Ask only what is missing — do not ask questions that were already answered. Ask one focused question at a time if multiple things are missing, or group closely related gaps into one round of questions.

3. Once all four areas are sufficiently covered, confirm the feature name and the target semver version with the user before writing the file. The feature name should be short, lowercase, hyphenated (e.g. `user-onboarding`, `payment-retry`). The version should follow semver (e.g. `1.0.0`).

4. Write the spec file to `specs/<feature-name>/<semver>/spec.md` in the repository root.

5. The spec file must contain all of the following sections in order:

   - **Overview** — a concise description of the feature and its purpose. Who it is for, what problem it solves, and what success looks like.
   - **Requirements** — a flat list of functional and non-functional requirements. Each requirement should be specific, testable, and unambiguous.
   - **User Stories** — one story per distinct user action or goal, using the format: `As a <user>, I want to <action> so that <outcome>.`
   - **Acceptance Criteria** — one or more criteria per user story, using the format: `GIVEN <context> WHEN <action> THEN <expected result>.`
   - **Flow** — one or more Mermaid diagrams illustrating the main user journey and any branching paths. Use `flowchart TD` for primary flows. Add a sequence diagram (`sequenceDiagram`) when system interactions (API calls, async steps, backend coordination) are part of the feature.

## Guard rails

- Do not begin writing the spec until all four essential questions are answered with enough precision to make each requirement testable.
- Do not invent user goals, system behaviors, or business rules that were not provided or confirmed by the user.
- Do not produce vague requirements like "the system should be fast" — every requirement must be concrete and verifiable.
- Do not skip the Mermaid flow — a spec without a visual representation of the user journey is incomplete.
- Do not write implementation details (technology choices, component names, API design) unless the user explicitly provides them as constraints.
- Do not conflate user stories with acceptance criteria — stories express intent and value, criteria express verifiable behavior.
- Do not proceed to writing if the feature name or semver version is not confirmed by the user.
- Do not overwrite an existing spec at the same path without warning the user and confirming they want to replace it.
