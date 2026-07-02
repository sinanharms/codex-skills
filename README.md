# Codex Skills

Local Codex skill collection for recurring development workflows.

This repository is meant to live at `~/.codex/skills`. Each top-level directory contains one skill with a `SKILL.md` instruction file and, when useful, supporting references, templates, examples, or gotchas.

## Skills

| Skill | Purpose |
|-------|---------|
| `caveman` | Compress responses while keeping technical accuracy. |
| `lazy-dev` | Apply minimal-diff, YAGNI-first engineering discipline. |
| `python-review` | Review Python design, OOP, dependency boundaries, and Pydantic usage. |
| `docs-generator` | Generate README, API, and architecture documentation from existing code. |
| `docs-scaffold` | Split raw project docs into structured, cross-linked documentation. |
| `init-python-project` | Scaffold a minimal `uv` Python project after collecting required inputs. |
| `create-app-context` | Scaffold Python settings, application context, boundaries, wiring, and tests from local project patterns. |
| `skill-builder` | Create well-structured skills with progressive disclosure and templates. |

## Layout

```text
.
+-- README.md
+-- caveman/
|   +-- README.md
|   +-- SKILL.md
+-- create-app-context/
|   +-- SKILL.md
|   +-- assets/
|   +-- references/
|   +-- agents/
+-- docs-generator/
|   +-- SKILL.md
+-- docs-scaffold/
|   +-- SKILL.md
|   +-- examples/
|   +-- references/
|   +-- templates/
+-- init-python-project/
|   +-- SKILL.md
|   +-- examples/
|   +-- references/
|   +-- agents/
+-- lazy-dev/
|   +-- SKILL.md
|   +-- gotchas.md
+-- python-review/
|   +-- SKILL.md
|   +-- gotchas.md
|   +-- references/
+-- skill-builder/
|   +-- SKILL.md
|   +-- examples/
|   +-- references/
|   +-- templates/
```

The `.system/` directory contains system-managed skills and is not the main content of this repo.

## Usage

Codex discovers skills from this directory automatically when it is installed as `~/.codex/skills`.

Invoke a skill by name when you want its workflow, for example:

```text
${skill_name}
or like this:
Use lazy-dev before this refactor.
Use python-review on this module.
Use init-python-project to create a new uv project.
/caveman full
```

Skill instructions are in each `SKILL.md`. Supporting files are intentionally local to the skill that needs them.

### Python review

Use `python-review` for maintainability reviews of Python modules, especially OOP/service boundaries, dependency injection, Pydantic models, settings, and refactor direction. For broader reviews it can fan out read-only subagents for architecture, data/config, tests/tooling, caller flow, and lazy-dev boilerplate checks, then merge those findings into one recommendation.

Reviews should finish with a recommended implementation plan and ask whether to implement it, verify it first, or revise the plan.

## Maintenance

No build step is required for this repo. Useful checks:

```bash
git status --short --branch
find . -maxdepth 3 -type f | sort
```

When editing a skill:

1. Keep `SKILL.md` focused on behavior and workflow.
2. Put large examples, templates, and references in subdirectories.
3. Update `gotchas.md` when a skill misses an important edge case.
4. Avoid adding dependencies or generated files unless the skill needs them.
