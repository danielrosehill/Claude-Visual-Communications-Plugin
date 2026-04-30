---
name: onboard-visual-project
description: Use when the user wants to set up a new visual-communications project for content enhancement.
---

# Onboard Visual Project

Set up a new visual-communications project for a whitepaper, blog post, technical document, magazine article, presentation, or other long-form content.

## When to use

- User wants to start a new visual-communications project
- User has content (markdown, PDF, URL, or text) and wants to plan visuals for it
- User needs to organize source material and visual assets for a specific piece

## Inputs to gather

- **Project name** — Short, descriptive identifier (will become the folder name)
- **Project type** — whitepaper | blog | technical-doc | magazine | presentation | other
- **Purpose/goal** — What is this content trying to achieve?
- **Target platform** — web | print | social | presentation | pdf
- **Source material** — File path, URL, Google Doc link, or pasted text
- **Audience** — Who will see this content? (technical, general, executive, student, mixed)
- **Visual style** — modern | minimalist | professional | technical | friendly | creative | editorial

## Procedure

1. **Collect project basics.** Ask the user for project name, type, and goal. Provide examples if needed (e.g., "Explain a new product to potential customers," "Thought leadership for LinkedIn").

2. **Determine target platform.** Clarify where the content will be published, as this affects resolution and format specifications.

3. **Acquire source material.** If provided as a file path, read it to understand content. If pasted text or URL, accept it directly.

4. **Gather audience and style.** Ask about target audience and desired visual aesthetic to inform later ideation and generation.

5. **Create project structure.** Create the directory at `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<project-name>/` with three subdirectories: `source/`, `visuals/`, `prompts/`.

6. **Write project.yaml.** Populate with:
   ```yaml
   name: <Project Name>
   type: <type>
   target_platform: <platform>
   purpose: <purpose statement>
   audience: <audience description>
   resolution:
     primary: <resolution>
     social: 1080x1080
   style_preferences:
     - <style1>
     - <style2>
   source_files:
     - source/<filename>
   created: <date>
   notes: |
     <any additional context>
   ```

7. **Save source material.** If provided as text, save to `source/` with an appropriate filename. If already a file, note the path reference.

8. **Summarize and next steps.** Confirm the project is ready and suggest running `/ideate-visuals` next.

## Output / side effects

- New project directory created under `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<project-name>/`
- Subdirectories `source/`, `visuals/`, `prompts/` created
- `project.yaml` written with project configuration
- Source material saved or referenced
- User is ready to proceed to ideation

## Safety / constraints

- Do not overwrite an existing project without confirmation.
- If source material is a file path, verify it exists before referencing.
- Keep notes clear and non-sensitive; this data is stored in the plugin directory.
