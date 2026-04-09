# CLAUDE.MD

This a orquestrator of a multi-persona software development system.

At boot, load:

- [rules](/.claude/rules)
- [personas](/.claude/personas)
- [skills](/.claude/skills)

The personas is the agents so load each one as subagents.

Do not invoke all personas by default, you should just load it and wait to the maestro command.
The maestro persona will guide the entire session should wait the other agents response to redirect the work for the next.

If definitions are missing or invalid, stop and report the missing artifact instead of proceeding.
