# convert-orquestrator

## Purpose

This skill converts the full `.claude` structure of this repository into the formats used by Cursor and Codex. It treats `.claude` as the single source of truth, updates generated artifacts in `.cursor` and `.codex`, and preserves the target conventions that are already part of the repository.

## Procedure

1. Inspect the full `.claude` tree before making changes.
2. Map each source artifact in `.claude` to its Cursor-compatible and Codex-compatible target output.
3. Treat `.claude` as the authoritative source for personas, rules, and other supported instruction files.
4. Convert `.claude/personas` into Cursor-compatible rule content and Codex-compatible persona content.
5. Convert `.claude/rules` into Cursor-compatible rules and any Codex-compatible instruction content supported by the target structure.
6. Update `.cursor/rules/*.mdc` outputs from the `.claude` source content.
7. Preserve known Cursor filenames that already exist, such as `00-maestro.mdc`, when overwriting mapped files.
8. Generate or update a Cursor-compatible `AGENTS.md` when the `.claude` source content provides an orchestration entrypoint or equivalent summary.
9. Generate or update `.codex/README.md` from the `.claude` source when the target structure requires a Codex-specific overview.
10. Generate or update `.codex/personas/*.md` from the `.claude/personas` source files.
11. Generate or update the root `AGENTS.md` when the converted Codex structure requires it.
12. Overwrite generated target artifacts in `.cursor` and `.codex` with the converted output instead of merging them by default.
13. Verify that the target files still reflect the current `.claude` structure after conversion.
14. Sumarize what you did and, if is applicable, what failed.

## Guard rails

- Do not treat `.cursor` or `.codex` as the source of truth when `.claude` already defines the content.
- Do not merge generated target files as the primary behavior when overwrite is possible.
- Do not rename existing mapped Cursor rule files when the repository already uses a preserved target filename.
- Do not skip parts of the current `.claude` tree during conversion without stating that limitation explicitly.
- Do not introduce unsupported `.claude` skill structures such as folder-based Codex skill packages.
- Do not generate target content that changes the intent of the source files instead of adapting their format.
- Do not overwrite unrelated files outside the mapped `.cursor`, `.codex`, and root `AGENTS.md` targets.
