# Installing Superpowers for Continue

## Prerequisites

- [Continue](https://continue.dev) VS Code or JetBrains extension installed

## Installation

### Step 1 — Clone the repository

Clone superpowers to a location Continue can read:

```bash
git clone https://github.com/obra/superpowers ~/.continue/superpowers
```

### Step 2 — Add the bootstrap rule

Add a rule to your Continue config (`~/.continue/config.yaml`) that points to the superpowers rules file:

```yaml
rules:
  - name: Superpowers
    rule: file://~/.continue/superpowers/.continue-plugin/rules/superpowers.md
```

Or copy the rule file directly into your global rules directory:

```bash
cp ~/.continue/superpowers/.continue-plugin/rules/superpowers.md ~/.continue/rules/superpowers.md
```

### Step 3 — Verify

Open a new Continue chat and send:

> Tell me about your superpowers

The assistant should describe the available skills and confirm it will check for them before taking action.

## Project-Level Installation

To activate Superpowers only for a specific project, copy or symlink the rule into the project's `.continue/rules/` directory:

```bash
# In your project root:
mkdir -p .continue/rules
cp ~/.continue/superpowers/.continue-plugin/rules/superpowers.md .continue/rules/superpowers.md
```

Or reference it in the project's `.continue/config.yaml`:

```yaml
rules:
  - name: Superpowers
    rule: file://<path-to-superpowers>/.continue-plugin/rules/superpowers.md
```

## Usage

Continue does not have a native `Skill` tool, so skills are accessed by reading `SKILL.md` files directly. When the assistant needs a skill, it reads:

```
~/.continue/superpowers/skills/<skill-name>/SKILL.md
```

Ask the assistant to use a specific skill:

```
Use the brainstorming skill to help me plan this feature.
Use the systematic-debugging skill to find this bug.
```

Or let it auto-trigger based on your request context — the bootstrap rule instructs it to check for relevant skills before any action.

## Updating

```bash
cd ~/.continue/superpowers && git pull
```

## Acceptance Test

Open a clean Continue chat and send:

> Let's make a react todo list

A working installation will trigger the `brainstorming` skill before writing any code. The assistant will ask clarifying questions to refine the spec before jumping into implementation.

## Troubleshooting

### Rule not loading

1. Verify the file path in your config.yaml is correct and the file exists
2. Check that Continue is reading the correct config file (`~/.continue/config.yaml`)
3. Restart VS Code after config changes

### Skills not found

The bootstrap rule instructs the assistant to read skills from the superpowers directory. If it can't find them, check that the clone path matches what you configured.

### Tool mapping

When skills reference Claude Code tools:
- `Skill` tool → read the `SKILL.md` file directly
- `TodoWrite` → track in conversation or create a checklist file
- `Task` (subagents) → no direct equivalent, complete steps sequentially
- File operations → `read_file`, `create_new_file`, `edit_existing_file`
- Shell → `run_terminal_command`

## Getting Help

- Report issues: https://github.com/obra/superpowers/issues
- Full documentation: https://github.com/obra/superpowers/blob/main/docs/README.continue.md
