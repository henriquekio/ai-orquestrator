---
description: This file describes the optional coding rules for react projects.
---

## Statement

- React components should be small, focused, and responsible for a single clear concern.
- Repeated or complex logic should be extracted into custom hooks or utilities when doing so improves reuse or readability.
- JSX should stay readable and easy to scan. Deeply nested markup and heavy inline logic should be avoided.
- Shared or non-trivial render logic should be moved out of inline JSX expressions when that improves comprehension.
- Composition and separation of concerns should be preferred over components that accumulate unrelated responsibilities.
- When it's aplicable, consider extract the logic to a custom hook, and keep the component focused on rendering.
- When it's aplicable, consider extract the reusable types to a `types` file in the same directory, and keep the component focused on rendering.
- When it's aplicable, use the theme and design system tokens and components to preserve visual consistency and reduce the need for custom styles.

## Rationale

Keeping components small and focused makes React code easier to understand, test, and change. Extracting repeated or complex logic into hooks or utilities helps reduce duplication and gives the codebase clearer boundaries between rendering concerns and reusable behavior.

Readable JSX and well-composed components improve maintainability and make reviews faster and safer. Favoring composition over large, multi-purpose components helps teams evolve features with less coupling and less accidental complexity.
