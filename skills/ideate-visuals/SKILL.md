---
name: ideate-visuals
description: Use when the user wants to brainstorm visual ideas for a project's source content.
---

# Ideate Visuals

Analyze source content and propose visual-communication concepts across multiple categories to enhance the piece.

## When to use

- User has set up a project with `/onboard-visual-project` and wants visual ideas
- User has content and wants brainstorming on how to visualize key concepts
- User wants to identify gaps in visual storytelling for a piece

## Inputs to gather

- **Project name** — If not active, ask which project to ideate for
- **Content review** — Optionally, ask if there are specific sections to focus on or types of visuals to emphasize

## Procedure

1. **Identify active project.** Check for project directories in `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/`. If multiple projects exist, ask the user which one to ideate for. Read its `project.yaml` for context.

2. **Read source material.** Load the source files referenced in the project config to understand the content, key sections, themes, and audience.

3. **Analyze structure.** Identify major topics, complex concepts, data points, and narrative arcs that would benefit from visual support.

4. **Propose 5–8 visual ideas.** Suggest concepts across these categories:
   - **Hero/Header Image** — Conceptual photography or illustration to set tone
   - **Explanatory Visuals** — Flowcharts, diagrams, infographics, before/after comparisons
   - **Conceptual Illustrations** — Metaphor-based, symbolic, or visual-analogy representations
   - **Data Visualizations** — Charts, graphs, data-driven infographics
   - **Spot Illustrations & Icons** — Small visuals to break text, reinforce points, section dividers
   - **Interactive/Animated** — Animated diagrams, scrollytelling, hover-reveal graphics
   - **Video Content** — Explainer segments, animated infographics, B-roll, text animations

5. **Detail each proposal.** For each visual, include:
   - Visual type and concept
   - Purpose (how it enhances the content)
   - Recommended placement in the document
   - Complexity: simple | medium | complex
   - Generation method: text-to-image | image-to-image | diagram | video | other

6. **Save ideation notes.** Write the proposals to `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<project-name>/ideation.md`.

7. **Solicit feedback.** Ask the user which visuals resonate, whether concepts should be expanded or modified, and any constraints or preferences to refine the list.

## Output / side effects

- Ideation markdown file written to `projects/<project-name>/ideation.md`
- 5–8 concrete visual concepts documented with placement and complexity
- User gains clarity on visual strategy for the content
- Ready to proceed to `/generate-visual-prompt` for chosen visuals

## Safety / constraints

- Read project.yaml to understand scope; do not invent concepts outside the content's theme.
- Keep suggestions diverse in type and complexity—include both quick wins and ambitious ideas.
