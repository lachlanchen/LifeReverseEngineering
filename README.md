# LifeReverseEngineering

LifeReverseEngineering (LRE) is a personal deep-research workspace that turns profile context into actionable outputs across three execution tracks:

- `learn` (LazyLearn): book plans and learning paths
- `earn` (LazyEarn): investment ideas and thesis tracking
- `IDEAS`: research directions and project concepts

The repo is designed for iterative runs with single-copy updates, so each cycle refreshes the latest artifacts instead of endlessly appending duplicates.

## Core Structure

```text
LifeReverseEngineering/
├── learn/            # LazyLearn submodule
├── earn/             # LazyEarn submodule
├── IDEAS/            # IDEAS submodule
├── notes/            # consolidated outputs (single-copy reports)
├── tools/            # self-heal logs and helper artifacts
└── website/          # static website for GitHub Pages
```

## Pipeline Logic

LRE runs as a staged pipeline (orchestrated by prompt tools in the parent AgInTi repo):

1. Profile stage: resolve identity anchors and evidence confidence.
2. Book stage: generate growth-focused reading recommendations.
3. Investment stage: draft opportunities, risk framing, and thesis notes.
4. Ideas stage: propose research/project directions with next actions.
5. Aggregation stage: build a single-copy markdown report.
6. Sync stage: write latest outputs into `learn`, `earn`, and `IDEAS`.
7. Reporting stage: produce final email/briefing content.

## Single-Copy Output Policy

This repo follows overwrite/update behavior for key summary files:

- Keep one current version of major notes.
- Replace old "latest" snapshots with new run outputs.
- Keep self-heal diagnostics in dedicated tool/log paths.

This makes daily/periodic runs clean, auditable, and easy to inspect.

## Website and Domain

The static site lives in:

- `website/index.html`

Custom domain target:

- `lre.lazying.art`

GitHub Pages deploy is handled via:

- `.github/workflows/static.yml`

Deployment uploads `website/` only (not the full repository root).

## Related Repositories

- AgInTi: orchestration and prompt-tool system
- LazyLearn (`learn/`): learning and reading outputs
- LazyEarn (`earn/`): investment outputs
- IDEAS (`IDEAS/`): research/idea outputs

## Status

LRE is active and optimized for:

- high-frequency iterative updates
- evidence-aware research summaries
- cross-repo output synchronization
