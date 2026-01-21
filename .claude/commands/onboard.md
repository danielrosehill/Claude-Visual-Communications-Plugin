# Visual Communication Project Onboarding

You are helping the user set up a new visual communication project. Guide them through the following steps to gather all necessary information.

## Step 1: Project Basics

Ask the user for:

1. **Project Name** - A short, descriptive name (will be used as the folder name)
2. **Project Type** - One of:
   - Whitepaper
   - Blog post
   - Technical document
   - Magazine article
   - Presentation
   - Other (specify)

3. **Purpose/Goal** - What is this content trying to achieve? Examples:
   - "Explain our new product to potential customers"
   - "Pitch to a tech magazine for publication"
   - "Internal training documentation"
   - "Thought leadership piece for LinkedIn"

## Step 2: Target Platform

Determine where this content will be published, as this affects image specifications:

- **Web/Blog** - Standard web resolution (1920x1080 or 1200x800)
- **Print Magazine** - High resolution (300 DPI minimum)
- **Social Media** - Platform-specific dimensions
- **Internal Presentation** - 16:9 slides
- **PDF Download** - Balance quality and file size

## Step 3: Source Material

Ask the user to provide their source content. This could be:

- A markdown file in the repository
- A Google Doc (they can share the link)
- A PDF document
- Pasted text directly in the conversation
- A URL to existing published content

If they provide a file path, read it to understand the content.

## Step 4: Audience & Style

Gather information about:

1. **Target Audience** - Who will see this content?
   - Technical professionals
   - General public
   - Business executives
   - Students/learners
   - Mixed audience

2. **Visual Style Preferences** - What aesthetic fits the brand/content?
   - Modern/minimalist
   - Technical/detailed
   - Friendly/approachable
   - Corporate/professional
   - Creative/artistic
   - Editorial/journalistic

## Step 5: Create Project Structure

Once you have gathered the information, create the project:

1. Create the project directory: `projects/{project-name}/`
2. Create subdirectories: `source/`, `visuals/`, `prompts/`
3. Create `project.yaml` with all gathered information
4. If source material was provided as text, save it to `source/`

## Example project.yaml

```yaml
name: "AI Ethics Whitepaper"
type: whitepaper
target_platform: web
purpose: "Educate business leaders about AI ethics considerations"
audience: "C-suite executives and business decision makers"
resolution:
  primary: 1200x800
  social: 1080x1080
style_preferences:
  - professional
  - modern
  - approachable
source_files:
  - source/whitepaper-draft.md
created: 2024-01-15
notes: |
  Focus on conceptual illustrations rather than technical diagrams.
  Brand colors: blue (#2563eb), gray (#64748b), white
```

## Completion

After creating the project, summarize what was set up and suggest next steps:

1. Run `/ideate` to brainstorm visual ideas for the content
2. Review and refine the visual concepts
3. Run `/prompt` to generate specific image prompts
4. Use the fal-ai MCP tools to generate the visuals

---

**Begin by greeting the user and asking about their project.**
