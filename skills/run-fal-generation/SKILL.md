---
name: run-fal-generation
description: Use when the user wants to execute a saved prompt against the fal-ai MCP and save the resulting image or video into the project.
---

# Run FAL Generation

Execute a saved prompt against the fal-ai MCP server to generate images or video, then save outputs to the project's visuals directory.

## When to use

- User has a finalized prompt saved in `prompts/` and wants to generate the visual
- User wants to iterate on a generation (multiple variations)
- User has visuals that need upscaling or image-to-image refinement

## Inputs to gather

- **Project name** — Which project to generate for (if not active)
- **Prompt slug** — Which saved prompt to use (from `prompts/` directory)
- **Model override** — Optional; user preference if different from prompt.yaml
- **Iteration notes** — Any tweaks to the prompt before generation

## Procedure

1. **Verify prerequisites.** Check that fal-ai MCP is installed and available. If not, direct the user to add it: "Install the fal-ai MCP server; see the Claude Code plugin documentation."

2. **Load project and prompt.** Read the active project's `project.yaml` and the selected `prompts/<slug>.yaml` to understand target specs and the prompt text.

3. **Determine generation type.** Inspect the prompt:
   - If model is `flux` or `sdxl`, use `generate_image` MCP tool
   - If model is `video`, use `generate_video` MCP tool
   - If marked as image-to-image, use `generate_image_from_image` with a reference image

4. **Validate technical specs.** Confirm aspect ratio and resolution match the project's target platform (from project.yaml).

5. **Call fal-ai MCP.** Invoke the appropriate MCP tool with:
   - Full prompt text (plus any negative prompt)
   - Model specified in the prompt YAML
   - Aspect ratio and resolution from settings
   - Any user-provided iteration notes merged into the prompt

6. **Receive and validate output.** Capture the generated file URL or local path from the MCP response.

7. **Save to visuals directory.** Download/move the generated image or video to `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<project-name>/visuals/` with a descriptive name (e.g., `hero-image-v1.png`, `explainer-video-final.mp4`).

8. **Update prompt YAML.** Append the generated file path to the prompt's `generated_files:` list:
   ```yaml
   generated_files:
     - ../visuals/hero-image-v1.png
   ```

9. **Report results.** Show the user the generated file, file size, and model used. Ask if they want to iterate or generate another prompt.

## Output / side effects

- Generated image or video saved to `projects/<project-name>/visuals/`
- Prompt YAML updated with `generated_files` entry
- User has a tangible visual asset ready for review or export
- Can iterate on prompts and re-generate as needed

## Safety / constraints

- MCP must be installed and working; gracefully handle connection errors.
- Do not overwrite existing visuals without user confirmation.
- Verify file paths before writing; ensure visuals directory exists.
- fal-ai MCP may have rate limits or quota—inform user if generation fails due to limits.
