---
name: claude-code-starter
description: One-shot setup for beginners/new machines. Installs CLAUDE.md, recommended skills, plugins, and usage docs.
trigger: /claude-starter
disable-model-invocation: true
---

# /claude-starter

Set up Claude Code best-practice configuration on a new machine or project.

## When to use

- New machine / fresh Claude Code install.
- Onboarding a teammate.
- Want a consistent baseline of rules, skills, plugins, and docs.

## Usage

```
/claude-starter              # interactive wizard
/claude-starter global       # install user-level CLAUDE.md + docs
/claude-starter project      # create ./CLAUDE.md for current project + docs
/claude-starter docs         # regenerate usage docs only
```

## What it installs

1. **CLAUDE.md** — global or project rules file.
2. **Recommended skills** — verifies they are present.
3. **Recommended plugins** — generates `/plugin install` commands (manual execution).
4. **USAGE.md** — quick-reference guide for everything installed.

## Safety rules

- Never overwrite an existing file without explicit user confirmation.
- Always read an existing file before offering to overwrite.
- If overwriting, create a timestamped backup first.
- Do not run `/plugin install` automatically; only generate the commands.

## Step-by-step workflow

### Step 1 — Determine mode

If `ARGUMENTS` is empty, ask the user:
- `global` — configure user-level `~/.claude/CLAUDE.md`
- `project` — configure `./CLAUDE.md` in the current working directory
- `docs` — regenerate usage docs only

If the argument is not one of these, tell the user it's invalid and show usage.

### Step 2 — Detect environment

Run:
```bash
mkdir -p "$HOME/.claude/claude-starter"
echo "$HOME/.claude"
```

Set:
- `CLAUDE_HOME = $HOME/.claude`
- `SKILL_DIR = $CLAUDE_HOME/skills/claude-code-starter`

### Step 3 — Install or update CLAUDE.md

Choose template based on mode:
- `global`: source = `$SKILL_DIR/templates/global-claude.md`, target = `$CLAUDE_HOME/CLAUDE.md`
- `project`: source = `$SKILL_DIR/templates/project-claude.md`, target = `./CLAUDE.md`
- `docs`: skip this step.

Read the source template. Then check if target exists:
- If target does not exist: write target with template content.
- If target exists: read target, show user the first 40 lines or a diff summary, and ask `overwrite / skip / backup-and-overwrite`. If backup, copy target to `target.<timestamp>.bak` before overwriting.

After writing, print:
```
Installed <mode> CLAUDE.md at <path>
```

### Step 4 — Verify recommended skills

Read `$SKILL_DIR/recommended-skills.md`. Parse each line starting with `- ` followed by a backtick skill name. For each skill name:
- Check if `$CLAUDE_HOME/skills/<name>/SKILL.md` exists.
- Record status: present / missing.

Do not install missing skills automatically. Print a table:
```
Recommended skills:
- using-agent-skills          present
- context-engineering         present
- spec-driven-development     missing
...
```

If any are missing, add them to the "Missing skills" section of the generated usage doc.

### Step 5 — Generate plugin install commands

Read `$SKILL_DIR/recommended-plugins.md`. Parse each line starting with `- ` followed by a backtick plugin spec like `plugin-name@marketplace`.

Generate two files:
- `$CLAUDE_HOME/claude-starter/install-plugins.sh`
- `$CLAUDE_HOME/claude-starter/install-plugins.ps1`

Each contains one command per plugin:
```bash
/plugin install commit-commands@claude-plugins-official
/plugin install code-review@claude-plugins-official
...
```

The PowerShell version uses the same `/plugin install ...` lines.

Also generate a markdown command list to embed in the usage doc.

Do not execute the commands.

### Step 6 — Generate usage docs

Read `$SKILL_DIR/USAGE.md` as the base. Create `$CLAUDE_HOME/claude-starter/USAGE.md` by copying the base and appending:

```markdown
## Current setup status

Generated: <ISO timestamp>

### CLAUDE.md
- Mode: <global|project|skipped>
- Path: <path>

### Skills status
<copy the table from Step 4>

### Plugin install commands
Run these in Claude Code:
```text
/plugin install commit-commands@claude-plugins-official
...
```
```

If mode is `project`, also write `./CLAUDE_USAGE.md` with the same content.

### Step 7 — Final report

Print a concise summary:
- What was created or updated.
- What was skipped.
- The exact commands the user should run next to install plugins.
- How to use the starter kit going forward (`/claude-starter docs` to refresh docs).

## Failure handling

- If `$SKILL_DIR` or any required bundled file is missing, stop and report the missing file path.
- If a read/write operation fails, report the error and stop.
- If the user declines to overwrite, skip that step and continue.
