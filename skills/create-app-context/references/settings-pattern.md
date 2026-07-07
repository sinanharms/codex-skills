# Settings Pattern

Use this when generating or modifying settings modules.

## Current Project Shape

The reference module is `src/app/settings.py`.

Project conventions:

- Import `from __future__ import annotations`.
- Use `pydantic_settings.BaseSettings`.
- Use `SettingsConfigDict` with `.env`, UTF-8, `extra="ignore"`, and case-insensitive environment names.
- Use typed fields with `Field(...)` descriptions for required operational values.
- Use `SecretStr` for sensitive values.
- Validate cross-field or normalized values with `@model_validator(mode="before")`.
- Expose a module-level `settings = Settings()` only when the package's import behavior can tolerate immediate environment validation.

## Generation Guidance

Keep settings focused on app/module configuration, not runtime objects. Do not place clients, connectors, or services on `Settings`.

Before adding a field, know:

- env var name and prefix;
- whether the field is required;
- default value, if any;
- validation rule;
- whether the value is secret;
- whether it participates in derived properties.

Use derived properties for stable computed values such as URLs. Raise clear `ValueError`s when required inputs for derived properties are missing.

## Settings Sanity Check

When docs are unavailable or the repo already has implementation, infer required settings from code before asking the user. Compare settings fields against:

- constructors and factory functions used by context/container code;
- direct `os.environ` or environment helper reads;
- URL/path/credential/provider arguments passed into clients, stores, connectors, registries, or services;
- tests that instantiate settings or monkeypatch environment variables;
- README or deployment examples, when present.

Flag two classes of issues:

- missing settings: discovered runtime configuration has no settings field and no other obvious source;
- unused settings: a settings field has no code consumer, derived property, test, or documented purpose.

Do not silently add speculative fields. If code shows a required value but the intended env var/name/default is unclear, ask one question and wait for the answer.

## Codex Workflow

Before editing settings:

1. Read existing settings modules and their callers.
2. Read docs for required runtime configuration, secrets, providers, and environment names when available.
3. If docs are missing or implementation already exists, scan constructors, factories, environment reads, entrypoints, and tests to infer required settings.
4. Identify missing decisions and sanity-check missing/unused settings.
5. Ask one question, wait for the answer, then continue.

Useful one-at-a-time questions:

- "Which settings are required before this module can start?"
- "Which optional settings should have defaults?"
- "Which of these settings are secrets?"
- "What validation should fail fast?"
- "Should this module instantiate `settings = Settings()` at import time?"
- "I found `<setting_name>` on settings but no consumer. Should it stay, be wired, or be removed?"

Do not introduce a setting just because a template contains a placeholder. Every field should have a known consumer or documented purpose.
