# Frontend Reviewer Review Template

Each review should stay focused on findings and risk. Use a structure like:

```md
# Review Scope

- Feature: <what was reviewed>
- Basis:
  - <requirements, architecture, or implementation reference>

## Findings

- Severity: <high | medium | low>
  - Issue: <problem>
  - Impact: <why it matters>
  - Location: <component, file, or behavior>
  - Recommendation: <what should change>

## Gaps

- Missing States:
  - <gap>
- Accessibility:
  - <gap>
- Tests:
  - <gap>

## Conclusion

- Status: <approved with notes | changes required>
- Residual Risks:
  - <remaining risk, if any>
```

If the approved architecture or requirements are missing, state that the review basis is incomplete and limit conclusions accordingly.
