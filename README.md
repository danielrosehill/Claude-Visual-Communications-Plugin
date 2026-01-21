# Claude Visual Communications Space

A Claude Code workspace template for enhancing long-form content with AI-generated visual communications.

## Overview

This workspace provides a structured workflow for adding visual elements to written content like whitepapers, blog posts, technical documents, and articles. The process follows two main phases:

1. **Ideation** - Brainstorming and planning visual elements
2. **Generation** - Creating visuals using AI image/video generation tools

## Quick Start

```bash
# Clone and enter the workspace
cd Claude-Visual-Communications-Space

# Start Claude Code
claude

# Set up a new project
/onboard

# Brainstorm visual ideas
/ideate

# Generate image prompts
/prompt
```

## Commands

| Command | Description |
|---------|-------------|
| `/onboard` | Initialize a new visual project with source material and settings |
| `/ideate` | Brainstorm and suggest visual communication methods for your content |
| `/prompt` | Generate optimized text-to-image or image-to-image prompts |

## Project Structure

```
Claude-Visual-Communications-Space/
├── CLAUDE.md              # Workspace instructions for Claude
├── README.md              # This file
├── .claude/
│   └── commands/          # Slash command definitions
│       ├── onboard.md
│       ├── ideate.md
│       └── prompt.md
└── projects/              # Your visual projects
    └── example-project/
        ├── project.yaml   # Project configuration
        ├── source/        # Original content
        ├── visuals/       # Generated images/videos
        └── prompts/       # Saved generation prompts
```

## Workflow

### 1. Onboarding (`/onboard`)

Start by running `/onboard` to create a new project. You'll provide:
- Project name and type (whitepaper, blog, etc.)
- Source material (markdown, Google Doc link, or pasted text)
- Target platform (web, print, social media)
- Style preferences
- Audience information

### 2. Ideation (`/ideate`)

Once your project is set up, run `/ideate` to brainstorm visual ideas. Claude will analyze your content and suggest:
- Hero/header images
- Explanatory diagrams and flowcharts
- Conceptual illustrations
- Data visualizations
- Spot illustrations and icons
- Interactive/animated elements
- Video content

### 3. Prompt Generation (`/prompt`)

After selecting visual concepts, run `/prompt` to create generation-ready prompts. The command:
- Creates optimized prompts for text-to-image models
- Handles image-to-image transformations
- Provides multiple prompt variations
- Saves prompts for reproducibility

## MCP Integration

This workspace uses the `fal-ai` MCP server for image generation. Available tools:

- `generate_image` - Create images from text prompts
- `generate_image_from_image` - Transform existing images
- `edit_image` - Make targeted edits to images
- `upscale_image` - Enhance image resolution
- `generate_video` - Create videos from prompts
- `generate_video_from_image` - Animate static images

## Resolution Guidelines

| Platform | Recommended | Notes |
|----------|-------------|-------|
| Web/Blog | 1920x1080 | Optimize for loading |
| Print | 300 DPI | CMYK-friendly colors |
| Social | 1080x1080 | Square works broadly |
| Slides | 1920x1080 | 16:9 aspect ratio |

## Example Project Config

```yaml
name: "AI Ethics Whitepaper"
type: whitepaper
target_platform: web
purpose: "Educate business leaders about AI ethics"
audience: "C-suite executives"
style_preferences:
  - professional
  - modern
  - approachable
source_files:
  - source/whitepaper-draft.md
```

## License

MIT
