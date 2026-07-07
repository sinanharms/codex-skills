---
name: create-app-context
description: Create project-style Python scaffolding for Settings, ApplicationContext, abstract boundaries, wiring, and tests. Use when adding a new app/module context modeled on this repo's src/app patterns, especially when docs or existing implementation should drive interface choices.
---

# Create App Context

Scaffold Python application/module structure that matches this repository's `src/app` conventions: Pydantic settings, an `ApplicationContext` model, dependency construction, confirmed abstract boundaries, wiring, and focused tests.

## Operating Rules

- Ask exactly one discovery question at a time. Stop and wait for the user's answer before asking another question.
- Read relevant project documentation before proposing abstract classes, protocols, or generated files. If docs are missing, stale, or thinner than the implementation, scan the repo and use existing code as the discovery source.
- Use existing code as the source of truth for naming, package layout, imports, validation style, and wiring.
- When the repo already has a full or partial implementation, inventory context-relevant classes before scaffolding: settings classes, context/container classes, service classes, clients, repositories, stores, connectors, registries, factories, entrypoints, and tests.
- Run a settings sanity check before edits: every setting field should have a known consumer or documented purpose, and every configuration value required by discovered context dependencies should be represented in settings or explicitly deferred.
- Treat templates in `assets/` as starter material only; adapt them to the discovered repo patterns.
- Present a dry-run plan before edits unless the user explicitly asks to write immediately.
- Do not overwrite existing files without explicit approval.
- Create an abstraction only when docs, code, or the user confirm the boundary.

## Workflow

1. **Load the local context.** Read relevant docs first when present: `README.md`, `AGENTS.md`, `docs/`, architecture notes, API contracts, story files, and design specs. Then read existing settings/container modules and nearby callers.
2. **Scan implementation when needed.** If docs are absent, incomplete, or the repo already contains a substantial implementation, scan the codebase for app-context candidates: settings classes, context/container classes, service/client/repository/store/connector/registry classes, factories, entrypoints, and tests. Use the scan to find all classes that need context construction or settings.
3. **Choose the next question.** Read `references/scaffold-questions.md`. Ask only the single highest-value missing question when the docs/code scan leaves a decision unresolved, then wait for the user's answer.
4. **Map settings and context.** Read `references/settings-pattern.md` before settings work and `references/context-pattern.md` before context work. Keep generated names and behavior consistent with the current repo. Sanity-check that discovered runtime configuration is covered by settings.
5. **Derive possible boundaries.** Read `references/abstract-classes-pattern.md` before proposing an abstract class or protocol. Present one candidate boundary at a time and wait for confirmation.
6. **Prepare a dry run.** Summarize files to create/update, classes/functions, settings/env vars, abstract boundaries, registrations, and tests. Include the implementation-derived class inventory and settings sanity-check result when repo scanning was used.
7. **Apply scoped edits.** Generate only the approved files/patches. Use `assets/*.tmpl` as examples, not as rigid output.
8. **Verify.** Run focused tests or lightweight import/compile checks for generated modules. If verification is skipped, state why.

## Resource Map

- `references/scaffold-questions.md`: one-question-at-a-time discovery tree.
- `references/settings-pattern.md`: project settings conventions and validation rules.
- `references/context-pattern.md`: application context construction conventions.
- `references/abstract-classes-pattern.md`: when to create abstract boundaries and what to ask.
- `assets/settings.py.tmpl`: starter settings module.
- `assets/container.py.tmpl`: starter context module.
- `assets/interface.py.tmpl`: starter abstract interface/protocol module.
- `assets/test_context.py.tmpl`: starter tests for settings/context construction.

## Completion

When done, report:

- files created or changed;
- abstract boundaries created, deferred, or rejected;
- verification commands and results;
- unresolved questions or deliberately skipped work.
