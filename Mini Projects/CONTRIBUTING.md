# Contributing

Thanks for your interest in contributing!

## How to propose a change
1. Open an issue first describing the change.
2. Create a branch from `main` like: `feat/short-name`.
3. Make your edits and include tests/notebooks if relevant.
4. Open a pull request and fill out the PR template.

## Code style
- Python: follow PEP8; prefer `ruff` or `flake8` for linting.
- Notebooks: keep outputs cleared before committing (`jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace file.ipynb`).

## Folder rules
- Put raw datasets under `data/` (gitignored).
- Reproducible scripts in `proj*/code/` with a README explaining how to run.
