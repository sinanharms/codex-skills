# User Input

Ask for these values before generating files. Ask sequentially: present only one question, wait for the user's answer, then ask the next unresolved question. Do not present the whole questionnaire at once unless the user explicitly asks for all questions up front.

- Project name: default example `myproject`.
- Destination path: where to create the folder.
- Package/import name: default to the project name normalized with hyphens replaced by underscores.
- Description: used in `pyproject.toml` and `README.md`.
- Python version: default `3.14`.
- Runtime dependencies: default none. Use an empty `dependencies = []` list unless the user names runtime packages.
- Dev dependencies: default `pre-commit>=4.5.0,!=4.5.1`, `pytest>=9.0.2`, `ruff>=0.15.20`, `ty>=0.0.55`.
- Whether to run `uv sync`.
- Whether to run `uv run pre-commit install`.

Normalize `[project].name` to lowercase hyphen-case. Normalize the package directory to a valid Python identifier.
