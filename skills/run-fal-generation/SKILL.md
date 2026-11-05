---
name: run-fal-generation
description: Use when the user wants to execute a saved prompt against the fal REST API and save the resulting image or video into the project's visuals directory.
---

# Run FAL Generation

Execute a saved prompt against fal's REST API with `$FAL_KEY` (run commands under `with-secrets`, or any shell that has `FAL_KEY` set), then save the output into the project's `visuals/` directory and update the prompt YAML. No MCP server is involved.

## When to use

- The user has a finalised prompt saved in `prompts/<slug>.yaml` and wants to generate the visual.
- The user wants to iterate on a generation or upload a reference for image-to-image.
- The user wants to look up pricing or pick a model before generating.

## fal REST routes

All calls send `Authorization: Key $FAL_KEY`.

Discovery:
- Search models: `GET https://api.fal.ai/v1/models?q=<keywords>&limit=5` (add `&category=text-to-image` etc.)
- Input/output schema: `GET https://fal.ai/api/openapi/queue/openapi.json?endpoint_id=<model id>`
- Price: `GET https://api.fal.ai/v1/models/pricing?endpoint_id=<model id>` (returns `unit_price`, `unit`)

Execution (queue API):
- Submit: `POST https://queue.fal.run/<model id>` with the input JSON. Returns `request_id`, `status_url`, `response_url`, `cancel_url`.
- Poll: `GET <status_url>` until `status` is `COMPLETED` (values `IN_QUEUE`, `IN_PROGRESS`, `COMPLETED`; failures carry `error`).
- Result: `GET <response_url>`.
- Cancel: `PUT <cancel_url>`.
- Use the URLs from the submit response as given. For a model id with a subpath (`fal-ai/flux/dev`) status and result use only `owner/app`, and a hand-built URL with the subpath returns 405.
- Short jobs may use the synchronous `POST https://fal.run/<model id>` instead.

Outputs are CDN URLs, not local paths. This skill downloads them.

Example:

```bash
with-secrets bash -c '
R=$(curl -s https://queue.fal.run/fal-ai/flux/dev -H "Authorization: Key $FAL_KEY" \
  -H "Content-Type: application/json" -d @input.json)
S=$(echo "$R" | jq -r .status_url); O=$(echo "$R" | jq -r .response_url)
until [ "$(curl -s -H "Authorization: Key $FAL_KEY" "$S" | jq -r .status)" = COMPLETED ]; do sleep 3; done
curl -s -H "Authorization: Key $FAL_KEY" "$O" > result.json'
```

## Inputs to gather

- **Project name** (or active project)
- **Prompt slug** — which `prompts/<slug>.yaml` to execute
- **Model** — from the prompt YAML, or override; if unsure, search with the models endpoint
- **Iteration notes** — any tweaks to merge into the prompt before submission
- **Reference image** — for image-to-image; local path, sent as a `data:` URI or staged to a URL

## Procedure

1. **Verify the key.** `FAL_KEY` must be set (`with-secrets bash -c 'test -n "$FAL_KEY"'`). If not, tell the user and stop.

2. **Load project + prompt.** Read `${CLAUDE_PLUGIN_DATA:-$HOME/.local/share/claude-plugins}/visual-communications/projects/<project>/project.yaml` and `prompts/<slug>.yaml`.

3. **Pick the model (if not set).** If the prompt YAML lacks a concrete fal model id (e.g. `fal-ai/flux/dev`, `fal-ai/flux-pro`, `fal-ai/minimax/video-01`), search the models endpoint with a keyword. Confirm the choice with the user if there's ambiguity.

4. **Sanity-check inputs and price.** Fetch the OpenAPI schema to confirm parameter names (image models commonly take `prompt`, `image_size` / `aspect_ratio`, `num_images`, `negative_prompt`; video models often take `prompt`, `image_url`, `duration`). Optionally query the pricing endpoint and surface the cost to the user before running.

5. **Reference images if needed.** For image-to-image or video-from-image, pass the local file as a `data:image/png;base64,...` URI in `image_url` / `image_urls` (check the schema for which). For large files, stage with `cloud-storage:stage-file` (`stage.sh <file>` gives a presigned URL; delete after) and pass that URL.

6. **Run the model.** Submit to the queue, poll `status_url`, fetch `response_url` (see routes above). The synchronous `fal.run` endpoint is fine for short jobs; use the queue for anything over ~60s, such as most video.

7. **Download the outputs.** Parse output URLs from the result (typical fields: `images[].url`, `video.url`, `audio.url`). For each, download to:
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

9. **Report.** Show the saved paths, the model id used, and the price (if the pricing endpoint was queried). Offer next steps: regenerate with tweaks, run a new prompt, or upscale an output (search the models endpoint for "upscale" if asked).

## Tips

- For Flux: `fal-ai/flux/dev` is a good default for stills; `fal-ai/flux-pro/v1.1` for higher fidelity.
- For video: most models are slow — use the queue API.
- For aspect ratios: pass the model's expected enum (`square_hd`, `landscape_16_9`, etc.) — the OpenAPI schema is the source of truth.
- Negative prompts: only some models accept `negative_prompt`; check the schema before passing it.

## Constraints

- Do **not** invent fal model ids or tool parameters — always verify via the models search and the OpenAPI schema first.
- Never overwrite existing files in `visuals/` without explicit user confirmation.
- If a job fails (rate limit, quota, NSFW filter, model error), surface the exact fal error message; don't retry silently.
- Pricing varies — for batch generations, confirm with the user before kicking off jobs that will run >5 images or any paid video.
