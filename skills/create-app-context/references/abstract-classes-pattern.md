# Abstract Classes Pattern

Use this before creating abstract base classes, protocols, or interface modules.

## Principle

Create an abstraction only for a real boundary confirmed by docs, code, or the user. Avoid interfaces that simply mirror one concrete class.

Read docs before proposing abstractions. Documentation often names the real boundary before code does: provider, repository, connector, registry, strategy, runner, client, store, gateway, or service.

Good abstraction signals:

- docs describe multiple providers, backends, stores, strategies, or external systems;
- tests need a fake implementation at a stable boundary;
- callers should not know which external service or storage provider is used;
- two existing implementations already share behavior;
- a future implementation is explicitly part of the user's requirement.

Weak abstraction signals:

- the only reason is "clean architecture";
- the name is a domain noun with no confirmed caller/implementation boundary;
- the interface would duplicate every method of a single concrete class;
- generated tests can mock a concrete object without losing clarity.

## ABC vs Protocol

Prefer `typing.Protocol` when structural typing is enough and implementations should not inherit from a base class.

Prefer `abc.ABC` when:

- the project already uses ABCs for this layer;
- shared base behavior or protected helpers are needed;
- explicit inheritance is useful for registration or readability.

Ask the user before choosing when the boundary is important.

## Codex Workflow

After reading docs and code, propose one candidate at a time:

"Should `<CandidateName>` represent the boundary between `<caller>` and `<implementation>`?"

If yes, ask:

"Should `<CandidateName>` be a `Protocol`, an `ABC`, or follow the existing style if one is present?"

Then ask:

"What concrete implementation should be wired first?"

If the user rejects a candidate, do not create a weaker version of the same abstraction. Continue with concrete wiring unless another documented boundary remains.
