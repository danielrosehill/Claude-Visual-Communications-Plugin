---
name: list-visual-projects
description: Use when the user wants to see all visual-communications projects with their status.
---

# List Visual Projects

Display all visual-communications projects in the plugin data store with current status.

## When to use

- User wants an overview of their projects
- User wants to see which projects have ideation complete, prompts generated, or visuals saved
- User wants to switch between projects or check project status

## Inputs to gather

None. This skill scans the project directory and reports what it finds.

## Procedure

1. **Scan project directory.** List all directories under `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/`.

2. **Check each project status.** For each project directory:
   - Read `project.yaml` to get name, type, platform, purpose
   - Check if `ideation.md` exists and is non-empty → "Ideation done"
   - Check `prompts/` directory for prompt files → "Prompts generated" with count
   - Check `visuals/` directory for image/video files → "Visuals saved" with count
   - Check if `source/` contains files → "Source loaded"

3. **Emit a table or summary.** Present as:
   ```
   Project Name        Type          Platform     Status
   ─────────────────────────────────────────────────────
   <name>              <type>        <platform>   <status>
   ```
   Where status is a comma-separated list of: ideation done, X prompts, Y visuals, source loaded

4. **Provide quick actions.** After the table, suggest commands:
   - `/ideate-visuals` to brainstorm for a project
   - `/generate-visual-prompt` to create a prompt
   - `/run-fal-generation` to generate visuals

## Output / side effects

- Formatted table or summary of all projects and their status
- No files modified or created
- User gains clarity on project inventory and next steps per project

## Safety / constraints

- Do not modify project files during scan.
- Handle gracefully if no projects exist (suggest running `/onboard-visual-project`).
