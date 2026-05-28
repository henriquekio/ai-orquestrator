# create-spec

## Purpose

Use this skill whenever a new feature, flow, or product change needs to be clearly defined before any implementation begins. It follows the Spec Driven Development (SDD) pattern: collect enough context to understand the problem, then produce a versioned spec file that gives the entire team — product, design, and engineering — a shared and unambiguous definition of what is being built and why.

A good spec prevents the most expensive kind of rework: building the right thing the wrong way, or the wrong thing entirely.

## Procedure

1. Read the context the user provided. A spec can only be as precise as the context behind it. Evaluate whether the following four areas are covered well enough to produce testable requirements:

   - **Who** will use this? (user type, role, situation)
   - **What problem** does it solve for them? (pain point, friction, unmet need)
   - **How** will they interact with it? (entry points, key actions, edge cases, unhappy paths)
   - **What outcomes matter?** (measurable goals, success signals, explicit non-goals)

2. If any area is missing or too vague, interview the user before writing anything. When you ask, briefly explain what you are trying to nail down and why it matters for the spec — users give better answers when they understand the intent behind the question. Ask one focused gap at a time, or group closely related gaps if they naturally belong together.

   Good context looks like: "Developers who just merged a PR want to see which review comments were addressed." Insufficient context looks like: "Users want to track changes." Push for the former.

3. Once the four areas are covered, propose a feature name and version before writing the file:
   - Feature name: short, lowercase, hyphenated (e.g. `payment-retry`, `user-onboarding`)
   - Version: semantic versioning (e.g. `1.0.0` for a new spec, `1.1.0` for a scope change)

   Confirm both with the user. If a spec already exists at the resulting path (`specs/<feature-name>/<semver>/spec.md`), warn the user before overwriting.

4. Write the spec file to `specs/<feature-name>/<semver>/spec.md` in the repository root.

5. The spec must contain all of the following sections in order:

   **Overview** — two to four sentences: who this is for, what problem it solves, and what success looks like. If someone reads only this section, they should understand the feature and its value.

   **Requirements** — a flat, numbered list. Every requirement must be specific and verifiable. "The button must show a spinner while `isLoading` is true" is a requirement. "The button should be fast" is not.

   **User Stories** — one story per distinct user goal or action:
   > `As a <user>, I want to <action> so that <outcome>.`

   **Acceptance Criteria** — one or more per user story, each expressing a verifiable behavior:
   > `GIVEN <context> WHEN <action> THEN <expected result>.`
   Criteria should be specific enough that a developer and a tester would independently reach the same conclusion about whether they pass.

   **Flow** — one or more Mermaid diagrams. Use `flowchart TD` for the primary user journey, including branching and error paths. Add a `sequenceDiagram` when the feature involves async steps, API calls, or multi-system coordination.

## Guard rails

Write only what the user has confirmed. Invented goals, behaviors, or business rules corrupt the spec and will mislead every agent and engineer who reads it downstream.

Keep requirements concrete. Vague requirements ("performant", "user-friendly", "scalable") cannot be tested and will produce disagreements at review time. If a requirement cannot be verified, it is not ready to be written.

User stories and acceptance criteria serve different purposes — do not conflate them. Stories capture intent and user value. Criteria capture observable, verifiable behavior. A story without criteria is a wish; criteria without a story are a checklist with no context.

Do not write implementation details (specific component names, technology choices, API design) unless the user explicitly provides them as constraints. Implementation is the engineer's domain; the spec defines the what and why, not the how.

Skip the Mermaid flow only if the feature has no branching paths and a single obvious outcome — and that is genuinely rare. A spec without a flow forces each reader to reconstruct the journey in their head, which leads to different interpretations.
