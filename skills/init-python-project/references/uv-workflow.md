# uv Workflow

Use `uv` after writing the template files:

- `uv sync` creates or updates `.venv`, installs dependencies, and creates/updates `uv.lock`.
- `uv lock` resolves the lockfile without installing when the user does not want environment sync.
- `uv run <command>` runs tools from the project environment.
- `uv run pre-commit install` installs hooks only when requested.

If `uv sync` fails because the selected Python version is unavailable, report the mismatch and ask whether to change `.python-version`/`requires-python` or install the requested interpreter.


-   repo: https://github.com/astral-sh/ty-pre-commit
    rev: v0.0.55
    hooks:
        - id: ty
        name: ty check
        entry: ty check .
        language: python
        pass_filenames: false
        types: [python]