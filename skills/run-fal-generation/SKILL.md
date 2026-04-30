---
name: run-fal-generation
description: Use when the user wants to execute a saved prompt against the official fal-ai MCP server and save the resulting image or video into the project's visuals directory.
---

# Run FAL Generation

Execute a saved prompt against the **official fal-ai MCP server** (https://mcp.fal.ai/mcp), then save the output into the project's `visuals/` directory and update the prompt YAML.

## When to use

- The user has a finalised prompt saved in `prompts/<slug>.yaml` and wants to generate the visual.
- The user wants to iterate on a generation or upload a reference for image-to-image.
- The user wants to look up pricing or pick a model before generating.

## Prerequisites: official fal-ai MCP

This skill targets fal's official remote MCP server. If it isn't connected, install it once:

```bash
claude mcp add --transport http fal-ai https://mcp.fal.ai/mcp \
  --header "Authorization: Bearer $FAL_KEY"
```

(Source: https://fal.ai/docs/documentation/setting-up/mcp — auth is a bearer token in the header; no npm package or env-var-only config.)

If `mcp__fal-ai__*` tools are not exposed in the current session, stop and instruct the user to run the command above with their fal API key.

## Tools exposed by the official server

Discovery:
- `mcp__fal-ai__search_models` — find models by keyword/category
- `mcp__fal-ai__get_model_schema` — full input/output schema for a model
- `mcp__fal-ai__get_pricing` — cost of running a model before you call it
- `mcp__fal-ai__search_docs` — search fal docs
- `mcp__fal-ai__recommend_model` — describe goal, get model suggestions

Execution:
- `mcp__fal-ai__run_model` — run a model and wait for the result (images, video, audio)
- `mcp__fal-ai__submit_job` — submit a long-running job, return a request ID
- `mcp__fal-ai__check_job` — poll status / fetch result / cancel

Utility:
- `mcp__fal-ai__upload_file` — upload a local file (or URL) to fal's CDN; returns a `cdn_url` usable as `image_url`/`audio_url` input

Outputs from `run_model` / `check_job` are returned as **CDN URLs**, not local paths — this skill is responsible for downloading them.

## Inputs to gather

- **Project name** (or active project)
- **Prompt slug** — which `prompts/<slug>.yaml` to execute
- **Model** — from the prompt YAML, or override; if unsure, call `recommend_model` or `search_models`
- **Iteration notes** — any tweaks to merge into the prompt before submission
- **Reference image** — for image-to-image; local path that needs `upload_file` first

## Procedure

1. **Verify the MCP is connected.** Check that `mcp__fal-ai__*` tools are available. If not, direct the user to the install command above and stop.

2. **Load project + prompt.** Read `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<project>/project.yaml` and `prompts/<slug>.yaml`.

3. **Pick the model (if not set).** If the prompt YAML lacks a concrete fal model id (e.g. `fal-ai/flux/dev`, `fal-ai/flux-pro`, `fal-ai/minimax/video-01`), call `recommend_model` with a one-line description, or `search_models` with a keyword. Confirm the choice with the user if there's ambiguity.

4. **Sanity-check inputs and price.** Call `get_model_schema` to confirm parameter names (image models commonly take `prompt`, `image_size` / `aspect_ratio`, `num_images`, `negative_prompt`; video models often take `prompt`, `image_url`, `duration`). Optionally call `get_pricing` and surface the cost to the user before running.

5. **Upload references if needed.** For image-to-image or video-from-image, call `upload_file` on the local reference and use the returned `cdn_url` as `image_url` in the model input.

6. **Run the model.**
   - Default: `mcp__fal-ai__run_model` (synchronous; preferred for short jobs)
   - Long-running (most video, large batches): `mcp__fal-ai__submit_job` → poll with `mcp__fal-ai__check_job` until status is `completed`. Use `submit_job` whenever the model's typical latency exceeds ~60s.

7. **Download the outputs.** Parse output URLs from the response (typical fields: `images[].url`, `video.url`, `audio.url`). For each, download to:
   ```
   ${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<project>/visuals/<slug>-vN.<ext>
   ```
   Use `curl -L -o <dest> <url>` (or `wget`). Auto-increment the `vN` suffix; never overwrite existing files without confirmation.

8. **Update the prompt YAML.** Append every saved file to `generated_files:`:
   ```yaml
   generated_files:
     - ../visuals/hero-vN.png
   model_used: fal-ai/flux/dev
   generated_at: 2026-04-30T22:15:00+03:00
   ```

9. **Report.** Show the saved paths, the model id used, and the price (if `get_pricing` was called). Offer next steps: regenerate with tweaks, run a new prompt, or upscale an output (call `recommend_model` with "upscale" if asked).

## Tips

- For Flux: `fal-ai/flux/dev` is a good default for stills; `fal-ai/flux-pro/v1.1` for higher fidelity.
- For video: most models are async — prefer `submit_job`/`check_job`.
- For aspect ratios: pass the model's expected enum (`square_hd`, `landscape_16_9`, etc.) — `get_model_schema` is the source of truth.
- Negative prompts: only some models accept `negative_prompt`; check the schema before passing it.

## Constraints

- Do **not** invent fal model ids or tool parameters — always verify via `get_model_schema` / `search_models` first.
- Never overwrite existing files in `visuals/` without explicit user confirmation.
- If a job fails (rate limit, quota, NSFW filter, model error), surface the exact fal error message; don't retry silently.
- Pricing varies — for batch generations, confirm with the user before kicking off jobs that will run >5 images or any paid video.
