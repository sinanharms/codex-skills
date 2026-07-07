# Refactor Patterns

Use these patterns as options, not automatic transformations.

## Functions to Service Class

Use when several functions share dependencies, configuration, cache, session, client, or lifecycle.

Prefer:
- a small constructor with explicit dependencies
- public methods named after use cases
- private helpers only when they remove duplication

Avoid:
- `Manager` or `Helper` classes with unrelated methods
- one-method classes with no state
- inheritance where composition is enough

## Raw Config to BaseSettings

Replace scattered environment access with one `pydantic-settings.BaseSettings` object when config is read in multiple places or needs validation/defaults.

Look for:
- repeated `os.getenv()`
- stringly typed booleans/ints/URLs
- import-time config reads that make tests hard
- secrets mixed into normal defaults

## Dicts to BaseModel

Use `pydantic.BaseModel` when a dict crosses a boundary or has a stable known shape.

Look for:
- `dict[str, Any]`
- repeated key strings
- validation spread across call sites
- serialization/deserialization logic near business code

## Hard-Coded Dependency to Injection

Move construction outward when code creates clients, repositories, clocks, filesystem handles, or API wrappers inside business logic.

Prefer constructor injection for objects reused across operations. Prefer parameter injection for one-off collaborators.

## Inheritance to Composition

If subclasses only vary one collaborator or strategy, prefer injecting that collaborator. Keep inheritance for true subtype relationships or framework-required extension points.

## Validator Placement

Use Pydantic validators for field normalization, cross-field validation, and external input cleanup. Keep workflow decisions, I/O, persistence, and policy orchestration outside validators.
