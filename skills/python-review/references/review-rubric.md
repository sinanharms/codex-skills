# Review Rubric

Use this rubric to review Python code for maintainability, not generic style trivia.

## First Pass

- What problem does this code solve, and is all current code needed?
- What are the public boundaries: API, CLI, DB, file, queue, env, LLM/tool call, or package API?
- What local conventions already exist for services, models, settings, dependency injection, and tests?
- Which checks already define style: Ruff, formatter, mypy, pyright, ty, pylint, or project docs?

## OOP Preference

Prefer OOP when it gives a stable home to state, behavior, lifecycle, or dependencies.

Good class candidates:
- Multiple functions pass the same group of dependencies or state.
- Behavior has a lifecycle: setup, run, teardown, cache, connection, transaction, session.
- There are multiple interchangeable implementations behind one interface.
- Tests need to swap a dependency without monkeypatching globals.
- A module has grown into unrelated functions and needs clear ownership boundaries.

Keep a function when:
- It is pure, stateless, and has one clear responsibility.
- A class would only wrap one method and no state.
- Dependency injection would add more ceremony than test value.
- The project already uses simple functions for this layer.

If OOP need is ambiguous, do not guess. Ask one targeted question, or present options with a recommendation.

## Pydantic-First Data Modeling

Prefer:
- `pydantic.BaseModel` for structured app data.
- `pydantic-settings.BaseSettings` for runtime configuration.
- Explicit fields and constrained types where validation matters.
- `model_validate()` at input boundaries and `model_dump()` at output boundaries.
- Pydantic validators for data normalization and validation, not broad business workflows.

Avoid:
- stdlib `dataclass` for app models.
- hand-written data container classes.
- raw `dict[str, Any]` when the shape is known.
- scattered `os.getenv()` calls outside settings objects.

Exception: a tiny private object can stay simple if Pydantic adds no validation, serialization, config, or boundary value.

## Dependency Direction

Prefer explicit dependencies over imports from global state. Constructor injection is usually clearest for long-lived services; parameter injection is usually clearest for small operations.

Use `Protocol` or a small abstract boundary when there are multiple real implementations or tests need a stable seam. Do not introduce abstract classes for a single concrete implementation unless the boundary is expected soon and the cost is low.

## Finding Quality

Every finding should answer:
- What is the maintainability risk?
- Where does it show in the code?
- What is the smallest useful change?
- What should remain unchanged?
