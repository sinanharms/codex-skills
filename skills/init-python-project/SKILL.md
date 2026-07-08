---
name: init-python-project
description: Create a minimal uv-managed Python project after collecting user inputs. Use when starting a new Python project with src layout, root tests, pyproject.toml, .gitignore, pre-commit, ruff, ty, pytest, and uv environment setup.
---

# Init Python Project

## Overview

Create a minimal Python project that follows this repo's tooling conventions: `uv`, `src/` layout, root-level `tests/`, `pyproject.toml`, `.gitignore`, `.pre-commit-config.yaml`, ruff, ty, pytest, and pre-commit. Always collect the user's project-specific inputs before creating files, asking one question at a time.

## Workflow

1. Ask for the required inputs in `references/user-input.md` sequentially. Ask only the next unanswered question, wait for the user's answer, then continue.
2. Confirm the destination path, especially if it already exists or is not empty.
3. Create the minimal layout shown in `examples/example-layout.md`.
4. Write files from `assets/templates/`, replacing placeholders with the user's answers. Place `test_smoke.py.tmpl` at `tests/test_smoke.py` in the repo root.
5. Run `uv sync` to create/update `.venv` and `uv.lock` when the user allows dependency resolution.
6. If the destination is not already a Git repository and the user wants hooks, run `git init` in the project root before installing hooks.
7. Run `uv run pre-commit install` only when the user asks to install hooks.
8. Verify with `uv run ruff format --check .`, `uv run ruff check .`, `uv run ty check .`, and `uv run pytest` when dependencies are installed.

## Required Inputs

Do not generate the project until these are known:

- project name
- destination path
- package/import name under `src/`
- short description
- Python version
- runtime dependencies, defaulting to none unless the user names packages
- dev dependencies
- whether to run `uv sync`
- whether to install pre-commit hooks

Use the defaults in `references/user-input.md` when the user wants the same setup as this repo.

## Gotchas

- Current workflow does not create a Git repository by itself.
- `uv run pre-commit install` fails outside a Git repo. If hooks were requested, initialize Git first with `git init` unless the target is already inside an existing repo.

## Resources

- `references/user-input.md`: questions, defaults, and normalization rules.
- `references/uv-workflow.md`: uv commands to use after file generation.
- `assets/templates/`: minimal project files to adapt.
- `examples/example-layout.md`: target layout.
