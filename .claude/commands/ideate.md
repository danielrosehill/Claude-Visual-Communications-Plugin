# Visual Ideation Session

You are conducting a creative ideation session to suggest visual communication methods for the user's content project.

## Pre-requisites

First, check if there's an active project:

1. Look for project directories in `projects/`
2. If a project exists, read its `project.yaml` to understand the context
3. Read the source material referenced in the project config
4. If no project exists, ask the user to either:
   - Run `/onboard` first to set up a project, OR
   - Provide the content directly for a quick ideation session

## Ideation Framework

Analyze the content and suggest visuals across these categories:

### 1. Hero/Header Images
The main visual that sets the tone for the piece:
- Conceptual photography
- Abstract representations of the main theme
- Metaphorical illustrations
- Atmospheric scene-setting images

### 2. Explanatory Visuals
Help readers understand complex concepts:
- **Flowcharts** - For processes, workflows, decision trees
- **Diagrams** - System architecture, relationships, hierarchies
- **Infographics** - Data presentation, comparisons, timelines
- **Annotated Screenshots** - For software/technical content
- **Before/After Comparisons** - For transformations, improvements

### 3. Conceptual Illustrations
Bring abstract ideas to life:
- Metaphor-based illustrations
- Symbolic representations
- Personification of concepts
- Visual analogies

### 4. Data Visualizations
For content with statistics or data:
- Charts and graphs (bar, line, pie, etc.)
- Data-driven infographics
- Comparative visualizations
- Progress/metric displays

### 5. Spot Illustrations & Icons
Small visuals that break up text and reinforce points:
- Custom icons for key concepts
- Section dividers
- Pull-quote illustrations
- Margin illustrations

### 6. Interactive & Animated
For digital-first content:
- Animated diagrams (GIF or video)
- Interactive web experiences
- Scrollytelling elements
- Hover-reveal graphics

### 7. Video Content
Moving image options:
- Explainer video segments
- Animated infographics
- B-roll style footage
- Text animation sequences

## Output Format

For each suggestion, provide:

1. **Visual Type** - Category from above
2. **Concept** - What the visual depicts
3. **Purpose** - How it enhances the content
4. **Placement** - Where in the document it would appear
5. **Complexity** - Simple (quick to generate) / Medium / Complex (may need iteration)
6. **Generation Method** - Text-to-image, diagram tool, video generation, etc.

## Example Output

```
## Suggested Visuals for "Introduction to Machine Learning"

### 1. Hero Image
**Concept:** Abstract neural network visualization with flowing data streams
**Purpose:** Sets a modern, technical tone while remaining approachable
**Placement:** Top of article, below title
**Complexity:** Medium
**Method:** Text-to-image (Flux)

### 2. Process Flowchart
**Concept:** ML pipeline from data collection to model deployment
**Purpose:** Gives readers a mental model of the full process
**Placement:** After "How ML Works" section
**Complexity:** Medium
**Method:** Diagram generation or structured prompt

### 3. Concept Illustration
**Concept:** Robot and human hands reaching toward each other (Michelangelo-style)
**Purpose:** Humanizes AI, makes it relatable
**Placement:** "Human-AI Collaboration" section
**Complexity:** Simple
**Method:** Text-to-image with style reference
```

## Conversation Flow

1. **Review the content** - Read and understand the source material
2. **Identify key sections** - Note the major topics/sections
3. **Present 5-8 visual ideas** - Varied types, prioritized by impact
4. **Discuss with user** - Get feedback, refine ideas
5. **Document selected visuals** - Save chosen concepts for `/prompt` phase

After presenting ideas, ask the user:
- Which visuals resonate most?
- Are there specific concepts they'd like visualized?
- Any style preferences or constraints?
- Should any ideas be expanded or modified?

---

**Begin by identifying the active project or asking for content to analyze.**
