# Visual Prompt Generation

You are creating optimized prompts for AI image and video generation. This command takes visual concepts (from ideation or user input) and transforms them into effective generation prompts.

## Prompt Types

### Text-to-Image
Creating images from descriptive text prompts. Used for:
- Hero images
- Conceptual illustrations
- Abstract visuals
- Scene generation

### Image-to-Image
Transforming or enhancing existing images. Used for:
- Style transfer
- Image enhancement
- Variations on a theme
- Compositing elements

### Video Generation
Creating motion content. Used for:
- Animated diagrams
- Explainer segments
- Dynamic visualizations

## Prompt Structure

Effective prompts follow this structure:

```
[Subject] + [Style] + [Composition] + [Lighting/Mood] + [Technical specs]
```

### Components

**Subject (What)**
- Main focus of the image
- Key elements and their relationships
- Actions or states

**Style (How)**
- Artistic style (photorealistic, illustration, 3D render, etc.)
- Reference artists or movements if helpful
- Color palette preferences

**Composition (Where)**
- Framing (close-up, wide shot, etc.)
- Perspective (eye-level, bird's eye, isometric)
- Layout and focal points

**Lighting/Mood (Feel)**
- Lighting type (natural, studio, dramatic, soft)
- Atmosphere (warm, cool, mysterious, bright)
- Emotional tone

**Technical (Specs)**
- Aspect ratio
- Resolution requirements
- Any specific technical needs

## Example Prompts

### Professional/Corporate
```
A diverse team of professionals collaborating around a holographic data visualization,
modern office environment with glass walls, soft natural lighting from large windows,
clean minimal aesthetic, shot from a slight low angle to convey empowerment,
muted blue and gray color palette with accent lighting, photorealistic style, 16:9 aspect ratio
```

### Technical/Diagram Style
```
Isometric 3D illustration of a cloud computing architecture,
showing servers, databases, and user devices connected by glowing data streams,
clean white background, flat design with subtle shadows,
tech blue (#2563eb) as primary color with gray accents,
minimal and professional, suitable for technical documentation, square format
```

### Conceptual/Abstract
```
Abstract visualization of artificial intelligence learning,
represented as a luminous neural network growing organically like a tree,
deep blue background transitioning to warm golden nodes,
ethereal and inspiring mood, digital art style with painterly touches,
centered composition with subtle particle effects, cinematic lighting
```

### Editorial/Magazine
```
Thoughtful portrait of a person interacting with an AI assistant displayed as soft light,
environmental portrait style, shallow depth of field,
warm afternoon light from a window, contemporary home office setting,
intimate and contemplative mood, magazine editorial photography style,
rule of thirds composition, 3:4 portrait orientation
```

## Workflow

1. **Gather Context**
   - Check for active project in `projects/`
   - Review ideation notes if available
   - Understand the visual concept to be generated

2. **Clarify Requirements**
   - What is the visual concept?
   - What style/mood is desired?
   - What are the technical requirements (size, format)?
   - Is this text-to-image or image-to-image?

3. **Generate Prompt Options**
   - Create 2-3 prompt variations
   - Vary style approaches
   - Include negative prompts if relevant

4. **Review & Refine**
   - Present prompts to user
   - Iterate based on feedback
   - Finalize the prompt

5. **Save & Execute**
   - Save finalized prompt to `projects/{name}/prompts/`
   - Optionally execute using fal-ai MCP tools

## Negative Prompts

For certain styles, negative prompts help avoid unwanted elements:

```
Negative: blurry, low quality, distorted, watermark, text,
logo, oversaturated, artificial looking, stock photo feel
```

## Model-Specific Tips

### Flux (Default)
- Excellent at following detailed prompts
- Good with photorealistic and artistic styles
- Handles text in images reasonably well

### SDXL
- Strong architectural and product imagery
- Good with specific art styles
- Benefits from style keywords

### Video Models
- Keep motion descriptions simple
- Specify camera movement explicitly
- Shorter prompts often work better

## Output Format

When presenting prompts, use this format:

```
## Prompt: [Visual Name]

**Concept:** Brief description of what we're creating

**Prompt:**
[The full generation prompt]

**Negative Prompt:** (if applicable)
[Elements to avoid]

**Recommended Settings:**
- Model: Flux / SDXL / etc.
- Aspect Ratio: 16:9 / 1:1 / etc.
- Style: Photorealistic / Illustration / etc.

**Notes:** Any additional guidance for generation
```

## Saving Prompts

Save finalized prompts to the project's prompts directory:

```yaml
# prompts/hero-image.yaml
name: "Hero Image - AI Collaboration"
created: 2024-01-15
model: flux
prompt: |
  [Full prompt text]
negative_prompt: |
  [Negative prompt if any]
settings:
  aspect_ratio: "16:9"
  style: photorealistic
generated_files:
  - ../visuals/hero-image-v1.png
  - ../visuals/hero-image-v2.png
notes: |
  v2 selected as final. Good balance of technical and approachable.
```

---

**Begin by asking what visual the user wants to create a prompt for, or check for ideation notes in the active project.**
