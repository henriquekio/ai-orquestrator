---
description: This file describes the TypeScript rules for the project.
---

## Statement

- All ts files MUST follow the good practices on type definitions, type annotations, and type inference.
- Every estructure MUST be typed, and every function MUST have its return type defined.
- It is prohibited to use the `any` type, and the use of `unknown` is discouraged.

## Rationale

Using TypeScript's type system effectively can help catch errors early, improve code readability, and enhance maintainability. By enforcing strict typing rules, we can ensure that our codebase is robust and less prone to runtime errors. Avoiding the `any` type encourages developers to think more carefully about the types they are working with, leading to better code quality and a clearer understanding of the data structures in use.
