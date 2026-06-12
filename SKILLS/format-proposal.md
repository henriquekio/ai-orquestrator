# format-proposal

## Purpose

Use this skill to transform a `proposal-estimator` output into a client-facing proposal document. The input is a technical work breakdown; the output is a clean, business-readable markdown that a client can understand without any engineering context.

The document presents the project name, a brief scope description, and a feature-by-feature breakdown — each with total hours and business-language task summaries — followed by the total hour count.

## Procedure

1. Read the estimate produced by `proposal-estimator`. Identify:
   - The project or client name
   - The overall scope of work
   - Each functional area with its hours and sub-tasks

2. If the project name is not clear from the estimate or context, ask the user before writing anything.

3. Write the scope section: two to three sentences describing the job to be done in business terms. Do not describe the technology stack or architecture. Describe the problem being solved and the capability being delivered to the end user.

4. For each work area in the estimate, produce a feature entry:
   - **Title line**: A short capability name written from the user's perspective, followed by the total hours for that area. Write what the feature does, not what engineering work it requires.
   - **Sub-items**: Two to five bullet points summarizing the tasks in business language. Each bullet describes what is being delivered or enabled, not how it is built. See the Business Language Guidelines section below.

5. Add a total line at the end.

6. Write the output to `proposals/<project-name>.md` in the repository root.

## Output Structure

```md
# <Project Name>

**Scope:** <Two to three sentences describing the job to be done in business terms.>

---

## <Feature Title> — <X>h

- <Business-language summary of what is delivered>
- <Business-language summary of what is delivered>

## <Feature Title> — <X>h

- <Business-language summary of what is delivered>

---

**Total: X hours**
```

## Business Language Guidelines

Translate technical tasks to outcomes the client can understand:

| Technical | Business |
|-----------|----------|
| Configure SQLite schema and CRUD repositories | Offline data storage so the app works without an internet connection |
| Implement sync queue with PENDING/SYNCED/FAILED states | Automatic background sync when the app reconnects to the internet |
| Guard routes using token validation | Restrict access to authenticated users only |
| Integrate expo-notifications and register device token | Push notification delivery to users' devices |
| Capture lat/lng/accuracy on check-in with permission handling | Mandatory GPS location capture on check-in and check-out |
| Detect Developer Options / USB Debugging on Android | Security controls to prevent usage on developer-mode devices |

Rules for the translation:
- Replace library and framework names with the capability they provide.
- Replace developer concepts (schemas, queues, guards, tokens) with user-facing behavior.
- Replace internal system states with what the user experiences.
- If a task genuinely has no user-facing equivalent (e.g. project setup), describe the enabling outcome: "Project foundation and development environment setup."

## Guard Rails

- Never include library names, framework names, or technology-specific terms in the client document.
- Never include implementation details such as schema names, API endpoints, or state management patterns.
- Never invent scope or capabilities not present in the original estimate.
- Never omit a work area — every area from the estimate must appear in the output.
- Never change hour counts — translate language only, never modify numbers.
- Never write sub-items as implementation steps. They must read as deliverables or outcomes.
