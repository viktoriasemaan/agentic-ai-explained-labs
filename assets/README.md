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

All are exports of the animated scenes in `internal/ai-gateway-scenes.html` and
`internal/agents-cost-scene.html` (0-indexed `?i=` scene numbers below; the scene
sources are kept local, outside the published repo).

| File | Used in | Source scene |
|---|---|---|
| `gateway-one-control-point.png` | 03, opening | `ai-gateway-scenes.html` i=3 "One control point" |
| `agent-parallel-spend.png` | 02, what this solves | `agents-cost-scene.html` i=0 "Parallel agents" |

The gateway scene deck has more scenes (tool sprawl i=0, the question i=1, create
endpoint i=5, several models i=6, system tables i=7, dashboard i=8, ask Genie i=9,
payoff i=10). They are not embedded in the guide by choice — regenerate any of them
with the pipeline below if a section ever needs one.

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
