# Visual Communications Space

This workspace is designed for enhancing long-form content projects (whitepapers, blog posts, technical documents) with AI-generated visual communications.

## Workflow

The visual communication process follows two main phases:

1. **Ideation** - Brainstorming and suggesting visual elements that would enhance the content
2. **Generation** - Creating the actual visuals using AI image/video generation tools

## Project Structure

Each project lives in its own directory under `projects/`:

```
projects/
  my-whitepaper/
    source/           # Original content (markdown, docs, PDFs)
    visuals/          # Generated images and videos
    prompts/          # Saved prompts for reproducibility
    project.yaml      # Project configuration
```

## Project Configuration

Each project has a `project.yaml` file:

```yaml
name: "Project Name"
type: whitepaper | blog | technical-doc | article | presentation
target_platform: web | print | magazine | social
purpose: "Brief description of the project's goal"
audience: "Target audience description"
resolution:
  web: 1920x1080
  print: 300dpi
  social: platform-specific
style_preferences:
  - "modern"
  - "minimalist"
  - "professional"
source_files:
  - source/main.md
notes: |
  Any additional context about the project
```

## Commands

### `/onboard` - Project Setup
Initialize a new visual communication project. Collects:
- Project name and type
- Source material location
- Target platform (affects resolution recommendations)
- Style preferences
- Project goals

### `/ideate` - Visual Brainstorming
Analyzes the source content and suggests visual communication methods:
- Infographics and data visualizations
- Flowcharts and diagrams
- Illustrations and concept art
- Photography-style images
- Icons and spot illustrations
- Videos and animations
- Interactive web experiences

### `/prompt` - Generate Prompts
Creates optimized prompts for image/video generation:
- Text-to-image prompts for various models (Flux, SDXL, etc.)
- Image-to-image enhancement prompts
- Style transfer suggestions
- Video generation prompts

## MCP Tools Available

This workspace uses the `fal-ai` MCP server for image generation:
- `generate_image` - Text-to-image generation
- `generate_image_from_image` - Image-to-image transformation
- `edit_image` - Edit existing images
- `upscale_image` - Enhance image resolution
- `generate_video` - Create videos from prompts
- `generate_video_from_image` - Animate static images

## Resolution Guidelines

| Platform | Recommended Resolution | Notes |
|----------|----------------------|-------|
| Web/Blog | 1920x1080 or 1200x800 | Optimize for fast loading |
| Print Magazine | 300 DPI, actual size | Request CMYK-friendly colors |
| Social Media | Platform-specific | Square (1080x1080) works broadly |
| Presentation | 1920x1080 | 16:9 aspect ratio |
| Whitepaper | 1200x800 or full-page | Balance quality and file size |

## Style Prompt Modifiers

When generating prompts, consider these style additions:

**Professional/Corporate:**
- "clean, modern design"
- "professional color palette"
- "minimal, elegant composition"

**Technical:**
- "technical illustration style"
- "blueprint aesthetic"
- "isometric 3D rendering"

**Editorial:**
- "editorial illustration"
- "magazine-quality photography"
- "conceptual art"

**Friendly/Accessible:**
- "warm, approachable style"
- "hand-drawn illustration feel"
- "friendly cartoon style"
