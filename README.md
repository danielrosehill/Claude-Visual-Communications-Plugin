# Visual Communications Plugin

Claude Code plugin for planning and prompt-engineering AI-generated visuals (images, diagrams, video) for whitepapers, blog posts, technical documents, and other long-form content.

Originally a workspace template (`Claude-Visual-Communications-Space`); now packaged as a plugin so it can be installed into any project. Project state lives under the plugin data-storage path, not the host repo.

## Installation

```bash
claude plugins install visual-communications@danielrosehill
```

## Skills

| Skill | Purpose |
|---|---|
| `onboard-visual-project` | Set up a new visual project — name, type, target platform, source material, audience, style. |
| `ideate-visuals` | Brainstorm 5–8 visuals (hero, explanatory, conceptual, data, spot, interactive, video) for a project's source content. |
| `generate-visual-prompt` | Convert a chosen visual concept into a model-optimised prompt (Flux / SDXL / video) with 2–3 variations and negative prompts. |
| `list-visual-projects` | Show all projects in the plugin data store with status (source / ideation / prompts / visuals). |
| `run-fal-generation` | Execute a saved prompt via the `fal-ai` MCP and save outputs to the project's `visuals/` directory. |
| `visual-style-reference` | Lookup resolution guidelines per platform and style-modifier vocabulary (professional / technical / editorial / friendly). |

## Data storage

Projects are stored under:

```
${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<name>/
  source/
  visuals/
  prompts/
  project.yaml
  ideation.md   # produced by ideate-visuals
```

## Dependencies

- **Optional**: official **fal-ai** remote MCP server (https://fal.ai/docs/documentation/setting-up/mcp) — required only by `run-fal-generation`. Install with:
  ```bash
  claude mcp add --transport http fal-ai https://mcp.fal.ai/mcp \
    --header "Authorization: Bearer $FAL_KEY"
  ```
  The other five skills work without it.

## Workflow

```
onboard-visual-project    → scaffolds projects/<name>/
ideate-visuals            → projects/<name>/ideation.md
generate-visual-prompt    → projects/<name>/prompts/<slug>.yaml
run-fal-generation        → projects/<name>/visuals/<file>
```

## Customising tool names

The skills name tools by their bare name on the `fal-ai` MCP server and work out the callable
name at run time. A direct install (`mcp__fal-ai__<tool>`) needs no setup. If your MCP client
or gateway names them differently, put a `config.json` in the plugin's data directory
(`$CLAUDE_USER_DATA/visual-communications/`, else `$XDG_DATA_HOME/claude-plugins/visual-communications/`, else
`~/.local/share/claude-plugins/visual-communications/`). It stays local and is never part of the plugin:

```json
{
  "tool_prefix": "mcp__mygateway__fal__",
  "tools": { "run_model": "generate_image", "search_models": "list_models", "get_model_schema": null },
  "notes": "No schema tool on this server: read the model page on fal.ai instead."
}
```

`run-fal-generation` is written for fal's official MCP (`run_model`, `submit_job`, `check_job`, …). If you reach fal through a different server, map each name in `tools`; `null` means "not available here", and the skill says so and follows `notes`.

## License

MIT — Daniel Rosehill.
