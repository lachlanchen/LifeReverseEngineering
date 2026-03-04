## Project Summary

LifeReverseEngineering (LRE) is a coordination repository for a three-track deep-research workflow: `learn` (learning outputs), `earn` (investment outputs), and `IDEAS` (research/publication outputs). The root repo acts as an aggregator and deployment surface, while most domain work lives inside Git submodules. Root-level artifacts emphasize a single-copy update model (`notes/lre_single_copy.md`) plus self-heal diagnostics (`tools/lre/*.json`, `*.log`).

## Repository Map

```text
LifeReverseEngineering/
├── README.md
├── .gitmodules                          # learn/earn/IDEAS submodule wiring
├── .github/
│   └── workflows/static.yml             # deploys website/ to GitHub Pages
├── website/
│   ├── index.html                       # root static landing page
│   ├── CNAME                            # lre.lazying.art
│   └── logos/
├── notes/
│   └── lre_single_copy.md               # consolidated latest run output
├── tools/
│   └── lre/
│       ├── profile_self_heal_latest.json
│       └── profile_self_heal_latest.log
├── i18n/                                # exists, currently empty
├── learn/                               # submodule (LazyLearn)
│   ├── README.md
│   ├── docs/                            # learn.lazying.art static site
│   ├── examples/                        # qaoa/vqe runnable Python scripts
│   ├── comp_physics/
│   ├── comp_physics_python/
│   ├── i18n/
│   └── tools/lre/books_self_heal_latest.json
├── earn/                                # submodule (LazyEarn)
│   ├── README.md
│   ├── docs/                            # earn.lazying.art static site
│   ├── investment/
│   ├── investment_pdfs/
│   ├── i18n/
│   └── tools/lre/investments_self_heal_latest.json
└── IDEAS/                               # submodule (IDEAS)
    ├── README.md
    ├── mkdocs.yml
    ├── scripts/
    │   ├── generate_site.mjs
    │   └── enable-hooks.sh
    ├── ideas/
    ├── publications/
    ├── docs/
    │   ├── ideas/*.html
    │   ├── publications/index.html
    │   └── assets/{ideas,publications,categories}.json + i18n/*.json
    ├── i18n/
    └── .github/workflows/pages.yml
```

## Key Components

- Root orchestration surface:
  - `README.md` defines LRE as a staged pipeline and single-copy output policy.
  - `.gitmodules` ties this repo to `learn`, `earn`, and `IDEAS` submodules.
  - `website/index.html` presents pipeline stages and links to deployed domain/repo.
- Output and diagnostics:
  - `notes/lre_single_copy.md` stores current consolidated report content.
  - `tools/lre/profile_self_heal_latest.json` captures remediation recommendations for profile-research tooling.
  - Track-specific self-heal snapshots exist in `learn/tools/lre`, `earn/tools/lre`, and `IDEAS/tools/lre`.
- Submodule implementation hubs:
  - `learn/` contains Python scripts, notebooks, textbook-code ports, generated figures, and a static docs site.
  - `earn/` contains a static frontend plus Markdown/LaTeX/PDF investment dossier workflow.
  - `IDEAS/` contains Markdown-to-publication flow (`ideas/` -> `publications/`) and a Node script that generates docs pages/manifests.

## Setup Signals

- Root-level:
  - Repository uses Git submodules (`.gitmodules`), so a fresh clone requires submodule initialization to fully populate `learn`, `earn`, and `IDEAS`.
  - No root `package.json`, `pyproject.toml`, or unified dependency lockfile exists.
- Deployment:
  - Root GitHub Action `.github/workflows/static.yml` deploys only `website/` to Pages.
  - `IDEAS/.github/workflows/pages.yml` sets up Node 18, installs `marked`, runs `node scripts/generate_site.mjs`, and deploys `IDEAS/docs/`.
- Tooling hints from submodule READMEs/files:
  - `learn`: Python 3 + optional Jupyter stack (`qiskit`, `pennylane`, `numpy`, `matplotlib`, etc.).
  - `earn`: static site requires no build; PDF workflow uses `pandoc` + `xelatex`.
  - `IDEAS`: publication builds use `latexmk`/`xelatex`; site asset generation uses Node script.

## Usage Signals

- Root usage flow is content/report-centric, not a single executable app:
  - Review/update generated summaries in `notes/` and diagnostics in `tools/`.
  - Publish root landing page updates via `website/` changes.
- Track-level usage patterns (as documented in submodule READMEs):
  - `learn`: run scripts from `examples/` (e.g., QAOA/VQE), iterate notebooks under `comp_physics/`.
  - `earn`: open `docs/index.html`, use `docs/pdf-viewer.html` routes, regenerate PDFs from `investment_pdfs/`.
  - `IDEAS`: edit `ideas/*.md`, compile publication TeX/PDF under `publications/<slug>/`, regenerate docs manifests/pages via `node scripts/generate_site.mjs`.

## Gaps/Unknowns

- Root `i18n/` directory exists but is empty in current state.
- No root `LICENSE` file present.
- No root automated test/lint workflow is defined; CI at root is deployment-focused.
- Root README references pipeline orchestration in a parent repo (AgInTi), but those orchestration scripts are not present in this repository.
- Self-heal state is uneven across tracks (example: `IDEAS/tools/lre/ideas_self_heal_latest.json` reports `missing_self_evolve_result`).
