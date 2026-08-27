# assets

Visuals pulled from the Agentic AI Explained scene files. All are exports of the
animated scenes, so the repo matches the videos exactly.

| File | Used in | Source |
|---|---|---|
| `unity-ai-gateway.gif` | README hero | `ai-gateway-scenes.html`, scene 4 "One control point", 6s at 12.5fps |
| `gateway-one-control-point.png` | 03, opening | same scene, still |
| `gateway-several-models-one-endpoint.png` | 03, endpoint section | scene 7 "Several models" |
| `gateway-system-tables.png` | 03, usage data section | scene 8 "System tables" |
| `gateway-spend-per-model-user-tool.png` | 03, Genie section | scene 11 "Payoff and CTA" |
| `agent-parallel-spend.png` | 02, opening | `agents-cost-scene.html` |

## Still missing

- A hero visual for lesson 1 (smart routing). The scene file for video 1 has not been
  exported yet. Placeholder comment sits in `01-smart-routing.md`.

## Re-exporting

The scene HTML files support deterministic frame capture through query params:
`file.html?i=<scene index>&t=<seconds>`. The page pauses every CSS and SVG animation,
seeks to `t`, and sets `document.body.dataset.ready="1"` when the frame is settled.
Screenshot `#stage` after that flag appears.

## Conventions

- Lowercase, hyphenated filenames.
- Reference with a relative path and real alt text describing what the diagram shows.
  Alt text is what answer engines and screen readers read.
- Keep GIFs under about 10 MB.
