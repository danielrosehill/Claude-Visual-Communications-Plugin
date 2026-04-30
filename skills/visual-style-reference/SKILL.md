---
name: visual-style-reference
description: Use when the user wants to look up resolution guidelines per platform or style modifier vocabulary for visual generation.
---

# Visual Style Reference

Display resolution guidelines for different publishing platforms and curated style-modifier vocabulary to enhance visual prompts.

## When to use

- User is planning a project and wants platform-specific resolution specs
- User is writing a prompt and wants style modifiers for professional, technical, editorial, or friendly aesthetics
- User wants to ensure visuals are correctly sized for their target platform

## Inputs to gather

Optional: user can ask about a specific platform or style category. If none provided, display full reference.

## Procedure

1. **Determine user need.** If user asks about a platform (web, print, social, presentation, whitepaper), show resolution guidelines for that platform. If asking about style (professional, technical, editorial, friendly), show vocabulary for that category.

2. **Display resolution guidelines.** Show the reference table:
   ```
   Platform                Recommended Resolution        Notes
   ──────────────────────────────────────────────────────────────────
   Web/Blog                1920x1080 or 1200x800         Optimize for fast loading
   Print Magazine          300 DPI, actual size          Request CMYK-friendly colors
   Social Media            Platform-specific             Square (1080x1080) works broadly
   Presentation            1920x1080                     16:9 aspect ratio
   Whitepaper              1200x800 or full-page         Balance quality and file size
   ```

3. **Display style modifier vocabulary.** Show categories with examples:
   ```
   Professional / Corporate
   • "clean, modern design"
   • "professional color palette"
   • "minimal, elegant composition"
   • "corporate aesthetic"
   • "sleek and polished"

   Technical / Detailed
   • "technical illustration style"
   • "blueprint aesthetic"
   • "isometric 3D rendering"
   • "schematic diagram style"
   • "engineering-focused composition"

   Editorial / Journalistic
   • "editorial illustration"
   • "magazine-quality photography"
   • "conceptual art"
   • "thought-provoking composition"
   • "narrative visual style"

   Friendly / Accessible
   • "warm, approachable style"
   • "hand-drawn illustration feel"
   • "friendly cartoon style"
   • "inviting and approachable"
   • "personable and relatable"
   ```

4. **Provide usage tips.** Explain that these modifiers can be mixed and combined in prompts to achieve a specific aesthetic (e.g., "professional + modern + warm" for a friendly corporate context).

5. **Answer follow-up questions.** If user asks for clarification on a platform or style, expand with additional examples or context.

## Output / side effects

- Reference tables and vocabulary displayed to user
- No files created or modified
- User has guidelines to make informed resolution and style choices for prompts and projects

## Safety / constraints

- This is a reference-only skill; no generation or file operations.
- Provide accurate, current platform specifications (may need periodic review as social platforms update specs).
