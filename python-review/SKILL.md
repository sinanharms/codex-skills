---
name: python-review
description: Review Python code for maintainable design. Use when asked to critique Python structure, OOP, DI, Pydantic models, or refactor direction.
version: 1.0.0
level: advanced
category: code-quality
---

# Python Review

Review Python code for maintainability, idiomatic structure, and pragmatic refactor direction. Use this skill to separate real design risk from taste, and to recommend the smallest useful improvement.

## Constraints

- Prefer OOP when it improves maintainability, ownership, testability, lifecycle management, or dependency boundaries.
- Do not force OOP when a function is clearer; if OOP need is ambiguous, ask a targeted question before recommending a class.
- Prefer `pydantic.BaseModel` for structured app data and `pydantic-settings.BaseSettings` for runtime configuration.
- Do not recommend stdlib `dataclass` unless project constraints forbid Pydantic or the object is trivial and strictly private.
- Never ask bulk question lists. Ask only the minimum blocking question, or present 2-3 concrete options with a recommendation.
- Preserve project conventions over generic Python advice.
- Do not rewrite code before reviewing the existing flow and callers.

## Phase 0 — Understand Context

Inspect the code path, callers, tests, and project tooling before giving design advice. Identify Python version, existing Pydantic usage, lint/type tooling, and local architecture conventions where available.

If the user's goal is ambiguous, ask one focused question. When options are clearer than an open question, present 2-3 choices and mark the recommended path.

## Phase 0.5 — Parallel Review

For non-trivial reviews, read `references/subagent-review.md` and dispatch focused read-only subagents before writing findings. Use subagents when the review spans multiple files, shared architecture, unclear callers, OOP/DI boundaries, Pydantic/settings, tests/tooling, or boilerplate/YAGNI risk.

Skip subagents for small single-file reviews unless the user explicitly asks for a deep review.

## Phase 1 — Review Design

Read `references/review-rubric.md` for the review criteria. Separate findings into must-fix correctness/maintainability issues, useful refactor candidates, and taste-only suggestions.

Read `references/refactor-patterns.md` when proposing OOP, dependency injection, Pydantic models, or settings refactors.

## Phase 2 — Respond

Read `references/output-format.md` for response shape. Lead with the highest-value recommendation, explain why it matters, and keep code examples small.

If proposing a change, include what should stay unchanged.
