# Agent Builder

Browser-based demo scaffolded from the `sanand0/scripts` demos skill: pick a workflow card, stream the architect plan as raw JSON via SSE, toggle the suggested datasets, upload your own context, and run every specialist agent with `lit-html` UI updates and markdown streaming.

## Features

- **Pure front-end stack** - `index.html` mirrors the reference navbar, hero, and settings layout, includes CDN import maps, and works from any static host.
- **Config-driven demos** - `config.json` exposes `demos[]` cards (icon, copy, problem brief, starter datasets) plus `defaults` for prompts, models, and max agents.
- **Custom briefs** - A “Bring Your Own Problem” form lets you stream the architect + agents against any ad-hoc statement without editing configs.
- **Stateful settings** - The collapsible form persists via `saveform`, so model and prompt overrides survive reloads and can be reset instantly.
- **LLM plumbing** - Credentials come from `bootstrap-llm-provider`, streaming is handled with a custom SSE decoder (mimicking the legacy repo), and agent responses render through `marked` + `highlight.js`.
- **Responsive UX** - Every streaming stage shows a Bootstrap spinner, flow nodes reflect live status, uploads stay local, and markdown output is safe-rendered with `unsafeHTML`.

## Getting Started

1. Open `index.html` in any modern browser (no build step required).
2. Click **Configure LLM** in the navbar and enter an OpenAI-compatible base URL plus API key (stored by `bootstrap-llm-provider`).
3. Optionally tweak the **Settings** form (model, architect prompt, agent style, max agents) - all values persist automatically via `saveform`.
4. Either pick a starter card **or** paste your own brief into *Bring Your Own Problem*, hit **Plan & Run**, review the architect plan + suggested datasets, attach/paste extra data, and press **Start Agents** to stream each specialist output while the flow nodes update live.

## Customization

- **Demos**: edit `config.json` -> `demos[]` to change card metadata or starter datasets. Keep synthetic CSV/JSON/Text blobs under ~1 MB each per the SKILL guidance.
- **Defaults**: adjust `config.json` -> `defaults` to control the initial model, architect prompt, agent style, or max-agents guardrail.
- **Logic/UI**: tweak `script.js` to change prompts, streaming behavior, or rendering. Because the app uses `lit-html`, all state changes funnel through `setState`.

## Deployment

The project is static and GitHub Pages friendly. Host the folder anywhere (Pages, Netlify, Vercel, S3, etc.) ensuring `config.json` sits beside `index.html`. No backend services are required - credentials and files stay local except for calls sent directly to the configured LLM endpoint.
