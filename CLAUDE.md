# Visual-Communications Plugin

A Claude Code plugin for planning and prompt-engineering AI-generated visuals (images, diagrams, video) for long-form content projects such as whitepapers, blogs, technical documents, and presentations.

## Overview

The plugin guides users through two phases of visual enhancement:

1. **Project onboarding** — Set up a project, gather source material, and define target platform and style
2. **Ideation & prompt generation** — Brainstorm visual concepts and convert them into optimized generation prompts
3. **Generation & management** — Execute prompts via the fal-ai MCP and manage visual assets

## Data Storage

All project data is stored in the plugin data directory:

```
${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/
  projects/
    <project-name>/
      source/            # Original content (markdown, PDFs, etc.)
      visuals/           # Generated images and videos
      prompts/           # Saved prompts (YAML format)
      project.yaml       # Project configuration
      ideation.md        # Brainstormed visual concepts
```

Each project's `project.yaml` defines:
- Project name, type (whitepaper | blog | technical-doc | magazine | presentation), and goal
- Target platform (web | print | social | presentation | pdf)
- Target audience and visual style preferences
- Resolution specifications per platform
- References to source material

## Skills

### onboard-visual-project
Set up a new project. Collects project name, type, purpose, platform, source material, audience, and style preferences. Scaffolds the project directory and writes `project.yaml`.

### ideate-visuals
Analyze source content and brainstorm 5–8 visual concepts across categories:
- Hero/header images
- Explanatory visuals (flowcharts, diagrams, infographics)
- Conceptual illustrations
- Data visualizations
- Spot illustrations and icons
- Interactive/animated content
- Video content

Saves ideation notes to `ideation.md` for later reference.

### generate-visual-prompt
Convert a visual concept into a detailed, model-optimized prompt. Provides:
- 2–3 prompt variations with different style approaches
- Negative prompts for unwanted elements
- Model-specific tips (Flux, SDXL, video)
- Technical specifications (aspect ratio, resolution)

Saves prompts as YAML to `prompts/<slug>.yaml`.

### list-visual-projects
Scan all projects in the data directory and display status:
- Ideation complete? (yes/no)
- Prompts generated? (count)
- Visuals saved? (count)
- Source loaded? (yes/no)

Useful for switching between projects and tracking progress.

### run-fal-generation
Execute a saved prompt using the fal-ai MCP server. Generates images or video and saves to the project's `visuals/` directory. Updates the prompt YAML's `generated_files` list for tracking. Detects missing MCP and directs user to install if needed.

### visual-style-reference
Display resolution guidelines per platform (web, print, social, presentation, whitepaper) and curated style-modifier vocabulary (professional, technical, editorial, friendly) for use in prompts.

## MCP Dependency

The plugin uses the **fal-ai** MCP server for image and video generation:
- `generate_image` — Text-to-image generation (Flux, SDXL, etc.)
- `generate_image_from_image` — Image-to-image transformation
- `edit_image` — Image editing
- `upscale_image` — Enhance resolution
- `generate_video` — Text-to-video generation
- `generate_video_from_image` — Animate static images

Ensure the fal-ai MCP is installed and configured before using `/run-fal-generation`.

## Typical Workflow

1. Run `/onboard-visual-project` to create a new project and load source material
2. Run `/ideate-visuals` to brainstorm visual concepts for the content
3. Review ideation and select promising concepts
4. Run `/generate-visual-prompt` to create generation prompts for chosen visuals
5. Run `/run-fal-generation` to execute prompts and save images/video
6. Iterate on prompts and regenerate as needed
7. Use `/list-visual-projects` to track progress across all projects
8. Refer to `/visual-style-reference` for platform specs and style modifiers

## Style Guidelines

The plugin supports multiple visual aesthetics:

- **Professional/Corporate** — clean, modern, minimal, professional color palette
- **Technical** — technical illustration, blueprint aesthetic, isometric 3D
- **Editorial** — editorial illustration, magazine-quality, conceptual art
- **Friendly/Accessible** — warm, approachable, hand-drawn, cartoon style

See `/visual-style-reference` for detailed modifier vocabulary.
