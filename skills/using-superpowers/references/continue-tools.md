# Continue Tool Mapping

Skills use Claude Code tool names. When you encounter these in a skill, use your Continue equivalent:

| Skill references | Continue equivalent |
|-----------------|---------------------|
| `Read` (file reading) | `read_file` |
| `Write` (file creation) | `create_new_file` |
| `Edit` (file editing) | `edit_existing_file` |
| `Bash` (run commands) | `run_terminal_command` |
| `Grep` (search file content) | `grep_search` |
| `Glob` (search files by name) | `file_search` |
| `Skill` tool (invoke a skill) | Read the `SKILL.md` file directly (see below) |
| `WebFetch` | `search_web` or `view_url` |
| `WebSearch` | `search_web` |
| `TodoWrite` (task tracking) | Track inline in conversation or write a checklist file |
| `Task` tool (dispatch subagent) | No direct equivalent — complete steps sequentially |
| Multiple `Task` calls (parallel) | Complete tasks sequentially, one at a time |
| `EnterPlanMode` / `ExitPlanMode` | No equivalent — stay in the main session |

## Loading Skills

Continue has no native `Skill` tool. When a skill applies, read its `SKILL.md` file and follow it directly:

```
read_file: <superpowers-install-path>/skills/<skill-name>/SKILL.md
```

Where `<superpowers-install-path>` is wherever superpowers was cloned (default: `~/.continue/superpowers`).

Available skills and their paths:
- `brainstorming/SKILL.md`
- `writing-plans/SKILL.md`
- `executing-plans/SKILL.md`
- `subagent-driven-development/SKILL.md`
- `test-driven-development/SKILL.md`
- `systematic-debugging/SKILL.md`
- `verification-before-completion/SKILL.md`
- `requesting-code-review/SKILL.md`
- `receiving-code-review/SKILL.md`
- `using-git-worktrees/SKILL.md`
- `finishing-a-development-branch/SKILL.md`
- `dispatching-parallel-agents/SKILL.md`
- `writing-skills/SKILL.md`

## Task Tracking Without TodoWrite

Since Continue has no `TodoWrite` tool, track multi-step tasks by:

1. Writing a checklist in a temporary markdown file:
   ```
   create_new_file: .superpowers-tasks.md
   ```
2. Or tracking state inline in the conversation using numbered lists.

## Subagents

Continue does not support dispatching subagents. Skills that use `dispatching-parallel-agents` or `subagent-driven-development` should be executed sequentially instead — complete each task one at a time in the same session.
