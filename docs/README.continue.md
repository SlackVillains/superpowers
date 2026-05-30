# Superpowers for Continue

This document covers the Continue-specific integration for Superpowers.

## What Works

| Feature | Status |
|---------|--------|
| Bootstrap rule injection | ✅ Via `.continue/rules/` |
| Skill loading (manual) | ✅ Read SKILL.md files directly |
| Skill auto-triggering | ⚠️ Relies on rule enforcement, no native tool |
| TDD / debugging workflows | ✅ Sequential execution |
| Subagent dispatch | ❌ Not supported — execute sequentially |
| TodoWrite task tracking | ⚠️ Workaround: write tasks to a file |

## How It Works

Superpowers in Continue uses the **rules** system to inject the bootstrap into every conversation. Continue injects rule files from `~/.continue/rules/` (global) or `.continue/rules/` (project-level) as persistent system-prompt instructions.

The bootstrap rule tells the assistant:
- That it has superpowers
- To check for relevant skills before acting
- How to load skills by reading `SKILL.md` files from disk
- Tool name mappings for Continue's agent tools

## Limitations vs. Claude Code

**No native Skill tool.** Claude Code has a `Skill` tool that loads and follows skills automatically. In Continue, the assistant must read skill files using `read_file`. This works but relies on the assistant remembering to check, rather than a hard tool call.

**No subagent dispatch.** Claude Code can spawn independent subagents. Continue's agent runs in a single session. Skills like `dispatching-parallel-agents` and `subagent-driven-development` fall back to sequential execution.

**No TodoWrite.** Continue has no equivalent for structured task tracking. The assistant uses inline lists or temporary markdown files as a workaround.

## Installation

See [.continue-plugin/INSTALL.md](../.continue-plugin/INSTALL.md) for the full install guide.

Quick version:

```bash
git clone https://github.com/obra/superpowers ~/.continue/superpowers
cp ~/.continue/superpowers/.continue-plugin/rules/superpowers.md ~/.continue/rules/superpowers.md
```

## Acceptance Test

Open a new Continue chat and send:

> Let's make a react todo list

A working integration will trigger `brainstorming` before writing any code — the assistant will ask clarifying questions to refine the design.

## Tool Mapping Reference

See [skills/using-superpowers/references/continue-tools.md](../skills/using-superpowers/references/continue-tools.md).
