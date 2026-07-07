# Scaffold Questions

Use this as a decision tree, not a bulk checklist. Ask exactly one question, wait for the user's answer, then decide the next question from the new state.

Do not paste this list to the user. Codex should use it privately to select the next missing decision.

## Start

If the target is unknown, ask:

- "What app or module name should I scaffold?"

Then ask only the next needed question from these areas.

## Documentation and Implementation Scan

Before asking about abstractions, read available docs when present. Prioritize:

- `AGENTS.md`;
- `README.md`;
- `docs/`;
- architecture or design specs;
- API contracts;
- domain notes;
- story files.

If docs mention possible services, repositories, connectors, providers, strategies, or external systems, turn those into candidate boundaries and confirm them one at a time.

If docs are missing, stale, or thinner than the code, scan the repo before asking the user. Find:

- settings classes and settings module instances;
- context/container classes and `create_context`-style factories;
- service, client, repository, store, connector, registry, provider, strategy, runner, and gateway classes;
- constructors that accept settings, clients, stores, registries, paths, URLs, credentials, or provider names;
- entrypoints, CLI commands, jobs, API startup code, and tests that construct dependencies.

Use the scan to build a private inventory of classes that should be wired into app context. Ask the user only when the scan leaves an unresolved decision, such as competing context modules, ambiguous dependency ownership, missing configuration names, or multiple possible implementations.

## Placement

- "Where should the generated files live?"
- "Should this create a new package or extend an existing package?"
- "Should package `__init__.py` files be created or updated?"

## Settings

- "Which settings are required for this module to start?"
- "Which settings are optional, and what defaults should they use?"
- "Which values are secrets?"
- "What environment prefix should these settings use?"
- "What validation rule should fail fast if configuration is invalid?"
- "I found `<Dependency>` needs `<value>` but no matching setting. Should I add `<setting_name>` or is it supplied another way?"

## Context Construction

- "Should this create a new `ApplicationContext`-style class or extend an existing one?"
- "Which dependencies should the context initialize?"
- "I found `<ClassName>` constructed by `<caller>`. Should app context own it?"
- "Should dependencies initialize eagerly during context creation or lazily on first use?"
- "Is cleanup or shutdown needed for any dependency?"
- "Does any dependency need async initialization?"

## Abstract Boundaries

Ask after reading docs and code:

- "Should `<CandidateName>` be an abstract boundary between `<caller>` and `<implementation>`?"
- "What concrete implementation should satisfy `<CandidateName>` first?"
- "Should this boundary be an `ABC`, a `Protocol`, or should it remain concrete for now?"

Skip abstraction questions when docs and code show only one concrete implementation and no stable caller/implementation boundary.

## Tests and Verification

- "Should I generate tests for settings validation, context construction, abstract contracts, or all of them?"
- "Should external clients be mocked, faked, or skipped in tests?"
- "Which test command should be used for this repo?"

## File Conflicts

- "If a target file already exists, should I merge, create a sibling file, or stop and ask?"
