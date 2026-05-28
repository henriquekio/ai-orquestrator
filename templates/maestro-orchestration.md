# Maestro Orchestration Template

Each orchestration cycle should stay explicit and minimal. Use a structure like:

```md
# Request Classification

- Type: <work type>
- Scope: <small, medium, large, multi-step, unclear>
- Constraints:
  - <constraint>

## Routing

- Agent: <specialist>
- Responsibility: <assigned scope>
- Inputs:
  - <artifact or dependency>

## Handoffs

- Completed:
  - <what came back>
- Pending:
  - <what still needs a specialist>
- Issues:
  - <conflict, ambiguity, or gap>

## Consolidated Output

- <final combined result or next execution step>
```

If the request is unclear, classify it as unclear, state what prevents safe routing, and avoid assigning fabricated work.
