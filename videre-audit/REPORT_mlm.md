# mlm — Technical Findings & Recommendations

Scope: Python utilities for tagging/embeddings (bm25, tagger, cards). Sources: `pyproject.toml`, `src/mlm/*`, `README.md` (empty).

Reference: Organization overview — videre-project on GitHub: https://github.com/videre-project

## Verified facts (evidence)
- Packages: `gql`, `h5py`, `pandas`, `scikit-learn`, `scipy`, `tqdm`.
- Modules include `bm25.py`, `tagger.py`, `cards.py`; `uv.lock` present for env reproducibility.

## Strengths
- Uses modern Python packaging (`pyproject.toml`) and uv lock.
- Clear separation of core modules.

## Risks / issues
- README empty → unclear usage, datasets, and licensing for corpora.
- No tests present → high risk of regressions.
- Data provenance and reproducibility not documented.

## Recommendations (prioritized)
1) Documentation & provenance
- Fill README with purpose, inputs/outputs, dataset lineage, licensing constraints.
- Add minimal examples and CLI usage.

2) Reproducibility & eval
- Pin models/artifacts; record seeds; add evaluation metrics and datasets.
- Integrate Weights & Biases or DVC for artifact tracking.

3) Testing
- Unit tests for BM25 scoring, tokenization, tagger behavior on fixtures.

## Quick wins (1 week)
- Add README with example, environment, and dataset notes.
- Add pytest + 3–5 unit tests for core functions.

## Suggested PRs
- PR1: "Docs & Examples".
- PR2: "Tests": pytest baseline.
- PR3: "Eval": add metrics script and sample report.
