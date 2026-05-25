# benchmark

## Purpose

This skill is used when the team needs to evaluate and compare external tools, libraries, or services before adopting one into the project. It drives a structured web research session that produces a factual comparison and a clear recommendation grounded in this project's stack, team size, and constraints. Use it when a technology decision requires evidence rather than assumption.

## Procedure

1. Identify the category of tool being evaluated and the specific constraints that matter for this project (free tier required, React Native / Expo compatible, fits existing patterns, etc.).
2. Search the web for the leading options in that category. Cast a wide net before narrowing.
3. For each candidate, collect only verifiable facts:
   - Pricing and free tier limits (seats, requests, MAUs, flags, etc.)
   - SDK availability and quality for React Native / Expo
   - Dashboard or management panel quality
   - Integration complexity relative to this project's stack (TypeScript, Expo, TanStack Query, NativeWind)
   - Known limitations, caveats, or community concerns
4. Produce a summary comparison table covering all candidates on the same dimensions.
5. Identify the top recommendation and a runner-up. State the reasoning explicitly — what makes the winner the right fit for this project specifically, not in general.
6. Flag any candidates that should be avoided and explain why.
7. Close with an open question to the team to confirm direction before any implementation begins.

## Guard rails

- Do not recommend a tool without searching for current pricing and SDK documentation — information in training data may be outdated.
- Do not present a recommendation without showing the comparison it is based on.
- Do not evaluate tools only on features — always include integration complexity relative to the existing stack.
- Do not recommend paid-only tools without explicitly noting the cost and flagging it as a constraint risk.
- Do not begin implementation as part of this skill — benchmarking ends with a recommendation, not with code.
- Do not skip the open question at the end — the team must confirm the direction before the next step.
- Do not omit self-hosted options when they exist and are relevant — they can change the cost equation entirely.
