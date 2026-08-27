# assets

Two kinds of visuals live here:

1. **Video explainer GIFs** — the animated explainer that accompanies each lesson's
   YouTube short. One per lesson.
2. **Scene stills** — frames pulled from the Agentic AI Explained scene files, so the
   written guides match the videos exactly.

## Video explainer GIFs

| File | Used in | Topic |
|---|---|---|
| `omnigent-explained.gif` | 01, hero | What the Omnigent meta-harness is |
| `ai-guardrails-explained.gif` | 02, hero | The guardrail / policy layer (allow, ask, deny) |
| `ai-governance-explained.gif` | 03, closing | The end-to-end governance picture |
| `unity-ai-gateway.gif` | README hero | "One control point" — every request through the gateway |

## Brand

| File | Used in | Notes |
|---|---|---|
| `databricks-logo-light.png` | README | Databricks primary lockup, full color (light backgrounds) |
| `databricks-logo-dark.png` | README | Databricks primary lockup, white (dark backgrounds) — swapped via `<picture>` |

## Scene stills

All are exports of the animated scenes in `ai-gateway-scenes.html` and
`agents-cost-scene.html` (0-indexed `?i=` scene numbers below).

| File | Used in | Source scene |
|---|---|---|
| `gateway-one-control-point.png` | 03, opening | `ai-gateway-scenes.html` i=3 "One control point" |
| `gateway-the-question.png` | 03, what this solves | i=1 "The question" |
| `gateway-tool-sprawl.png` | 03, what this solves | i=0 "Tool sprawl" |
| `gateway-create-endpoint.png` | 03, creating an endpoint | i=5 "Create an endpoint" |
| `gateway-several-models-one-endpoint.png` | 03, creating an endpoint | i=6 "Several models" |
| `gateway-system-tables.png` | 03, usage data | i=7 "System tables" |
| `gateway-ask-genie.png` | 03, asking Genie | i=9 "Ask Genie" |
| `gateway-dashboard.png` | 03, asking Genie | i=8 "Dashboard" |
| `gateway-spend-per-model-user-tool.png` | 03, payoff | i=10 "Payoff and CTA" |
| `agent-parallel-spend.png` | 02, what this solves | `agents-cost-scene.html` i=0 "Parallel agents" |

## Re-exporting the scene stills

The scene HTML files support deterministic frame capture through query params:
`file.html?i=<scene index>&t=<seconds>`. The page pauses every CSS and SVG animation,
seeks to `t`, and sets `document.body.dataset.ready="1"` when the frame is settled.
Screenshot `#stage` (1080×1920) after that flag appears.

Reproducible pipeline used to (re)generate the stills and the `unity-ai-gateway.gif`
hero (headless Chrome at 2× + a two-pass palette GIF encode):

1. Render each scene to a settled PNG:
   `chrome --headless=new --force-device-scale-factor=2 --window-size=1080,1976 \
   --virtual-time-budget=2500 --screenshot=out.png "file://…?i=<i>&t=<t>"`
2. Crop to the content box (title through caption) and scale for the docs.
3. For the hero GIF: render a 15 fps frame sequence, then
   `ffmpeg … palettegen=max_colors=256:stats_mode=full` followed by
   `ffmpeg … paletteuse=dither=sierra2_4a:diff_mode=rectangle -loop 0`.

## Conventions

- Lowercase, hyphenated filenames.
- Reference with a relative path and real alt text describing what the diagram shows.
  Alt text is what answer engines and screen readers read.
- Keep GIFs under about 10 MB (GitHub's inline-image cap).
