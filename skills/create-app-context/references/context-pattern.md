# Context Pattern

Use this when generating an `ApplicationContext`-style module.

## Current Project Shape

The reference module is `src/app/container.py`.

Project conventions:

- Import `from __future__ import annotations`.
- Model the context as a Pydantic `BaseModel`.
- Set `ConfigDict(arbitrary_types_allowed=True)` when storing concrete clients and services.
- Put dependency construction in `create_context(settings: Settings)`.
- Use small helper functions for dependencies that need validation before construction.
- Initialize external systems before constructing dependent services.
- Log initialization steps with `loguru.logger`.
- Return the full context object at the end.

## Generation Guidance

Build dependencies in dependency order. If a later service requires a connector, registry, or artifact store, construct those first and pass them explicitly.

When the repo already has implementation, scan before editing and identify every class that should be considered for context ownership. Prioritize classes that are:

- repeatedly constructed by entrypoints, jobs, handlers, or tests;
- constructed with settings, paths, URLs, credentials, provider names, clients, stores, or registries;
- long-lived services, clients, repositories, stores, connectors, registries, runners, or gateways;
- currently initialized in scattered places but needed by application startup.

Do not move a class into context solely because it exists. Leave pure data models, DTOs, exceptions, local helpers, and short-lived command objects outside context unless existing code clearly treats them as shared dependencies.

Keep construction readable. Prefer named variables and direct constructor calls over generic containers or reflection unless the repo already uses those patterns.

Use `Any` only when the concrete type is unavailable or external runtime behavior makes static typing impractical. Prefer concrete types or confirmed abstract interfaces when possible.

## Codex Workflow

Before editing a context module:

1. Read existing `container.py` files and entrypoints that call `create_context`.
2. Read docs to identify lifecycle, provider, and dependency-order constraints when available.
3. If docs are absent or the repo already has a substantial implementation, scan the codebase for classes and factories that already construct app dependencies.
4. Determine whether the requested work extends an existing context or creates a new one.
5. Cross-check the context inventory against settings so required configuration is present before wiring.
6. Ask one question, wait for the answer, then continue.

Useful one-at-a-time questions:

- "Which dependencies should this context expose?"
- "I found these context-owned candidates: `<names>`. Which, if any, should be excluded?"
- "Which dependency must be initialized first?"
- "Should any external system be initialized before object construction?"
- "Should construction fail fast if a setting is missing?"
- "Should this dependency be typed as concrete, abstract, or `Any`?"
- "Does this context need shutdown or cleanup behavior?"

Keep wiring explicit. If dependency construction becomes hard to scan, split only the validation/build steps that have their own failure modes.
