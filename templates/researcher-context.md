# Researcher Context Template

Each `context.md` should stay factual and compact. Use a structure like:

```md
# <path>

## Observed

- Type: <file or directory type if clear>
- Imports:
  - <import path>
  - <import path>
- Exports:
  - <explicit export if clear>
- References:
  - <local path or dependency>

## Unclear

- <state what cannot be determined from the code>
```

If the target is a directory, summarize only what is directly supported by the covered files inside that directory. If there is not enough evidence to explain the directory, say that its purpose is unclear.
