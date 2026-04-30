---
name: generate-visual-prompt
description: Use when the user wants to convert a chosen visual concept into an optimised text-to-image, image-to-image, or video prompt.
---

# Generate Visual Prompt

Transform a visual concept into a detailed, model-optimized prompt for image or video generation with 2–3 variations and model-specific guidance.

## When to use

- User has selected a visual from ideation and wants a generation prompt
- User wants to refine a prompt for a specific generation model (Flux, SDXL, video)
- User wants multiple prompt variations to explore different interpretations

## Inputs to gather

- **Visual concept** — Description of the visual to create (or reference to ideation.md)
- **Project context** — Project name (if not active) and any style/brand constraints from project.yaml
- **Preferred model** — Flux | SDXL | video | user preference
- **Technical specs** — Desired resolution, aspect ratio, format
- **Iteration constraints** — Any elements to emphasize or avoid

## Procedure

1. **Load project context.** Check for an active project; if not, ask the user to specify. Read `project.yaml` for style preferences, target platform, and resolution guidelines.

2. **Clarify the visual concept.** If the user references an idea from `ideation.md`, read that file. If providing a new concept, confirm the visual type, mood, and purpose.

3. **Determine generation method.** Identify whether this is text-to-image, image-to-image, or video generation based on the concept and user intent.

4. **Structure the prompt.** Use this framework: **[Subject] + [Style] + [Composition] + [Lighting/Mood] + [Technical Specs]**
   - **Subject** — Main focus, key elements, actions or states
   - **Style** — Artistic style (photorealistic, illustration, 3D render, etc.); color palette; reference artists if appropriate
   - **Composition** — Framing (close-up, wide, etc.); perspective; layout and focal points
   - **Lighting/Mood** — Lighting type; atmosphere; emotional tone
   - **Technical** — Aspect ratio, resolution, any platform-specific needs

5. **Generate 2–3 prompt variations.** Create variations that:
   - Explore different style approaches or moods
   - Vary composition or emphasis
   - Test model-specific keyword strategies

6. **Add negative prompts.** If relevant, include negative prompts to avoid unwanted elements (blurry, low quality, watermarks, oversaturated, stock photo feel, etc.).

7. **Provide model-specific tips.** Recommend:
   - **Flux** — Excellent at detailed prompts, photorealistic and artistic styles, handles text reasonably
   - **SDXL** — Strong for architecture and product imagery, benefits from style keywords
   - **Video** — Keep motion simple, specify camera movement, shorter prompts often work better

8. **Save the prompt YAML.** Write to `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<project-name>/prompts/<slug>.yaml`:
   ```yaml
   name: <Visual Name>
   created: <date>
   model: <flux | sdxl | video>
   prompt: |
     <full generation prompt>
   negative_prompt: |
     <optional negative prompt>
   settings:
     aspect_ratio: <ratio>
     style: <style>
     resolution: <resolution>
   variations:
     - prompt: |
         <variation 2>
     - prompt: |
         <variation 3>
   generated_files: []
   notes: |
     <any additional guidance or iteration notes>
   ```

9. **Present to user.** Show all prompts with recommended settings. Solicit feedback, iterate if needed, and finalize.

## Output / side effects

- Prompt YAML saved to `projects/<project-name>/prompts/<slug>.yaml`
- 2–3 prompt variations documented with model recommendations
- `generated_files` list initialized (to be populated after generation)
- Ready for `/run-fal-generation` to execute

## Safety / constraints

- Follow target-platform resolution guidelines from project.yaml.
- Do not include sensitive or private information in prompts.
- Test model-specific tips; some models may benefit from more or fewer descriptors.
