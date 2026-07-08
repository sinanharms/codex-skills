# uv Workflow

Use `uv` after writing the template files:

- `uv sync` creates or updates `.venv`, installs dependencies, and creates/updates `uv.lock`.
- `uv lock` resolves the lockfile without installing when the user does not want environment sync.
- `uv run <command>` runs tools from the project environment.
- `uv run pre-commit install` installs hooks only when requested, but it requires a Git repository.
- If the generated project is not already inside a Git repository and hooks were requested, run `git init` in the project root before `uv run pre-commit install`.

If `uv sync` fails because the selected Python version is unavailable, report the mismatch and ask whether to change `.python-version`/`requires-python` or install the requested interpreter.
