@AGENTS.md

## Claude Code notes
- The shared rules above come from `AGENTS.md`. Edit that file for anything every tool should follow. Keep this file for Claude-specific behavior only.
- Use plan mode for changes that touch more than two files, and wait for approval of the plan before editing.
- Run the **Commands** from the shell and read their output instead of predicting it.
- Rules are guidance, not enforcement. Put anything that must always happen (formatting, blocking edits to protected paths) in a hook in `.claude/settings.json`.
- Personal overrides go in `CLAUDE.local.md`, which you add to `.gitignore`. Run `/memory` to see which instruction files are loaded.
- Run `/clear` between unrelated tasks so old context does not steer new work.
- When you make the same mistake twice, propose one new line for **Known agent mistakes** in `AGENTS.md`.
