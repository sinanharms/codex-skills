# Subagent Review

Use subagents to speed up broad reviews, not to outsource judgment. The main agent owns the final recommendation, reconciles conflicting notes, and filters taste-only comments.

## When to Dispatch

Dispatch 2-3 read-only `explorer` subagents when the review has independent areas:

- multiple changed files or modules
- unclear caller flow or public boundaries
- OOP, dependency injection, or lifecycle concerns
- Pydantic model, settings, raw dict, or env handling concerns
- test, typecheck, lint, or regression-risk concerns
- boilerplate, over-abstraction, or YAGNI risk

Skip subagents for small single-file reviews unless the user asks for a deep review.

## Roles

- **Architecture explorer**: ownership, module boundaries, OOP/service shape, dependency direction.
- **Data/config explorer**: Pydantic models, settings, raw dict/env/config issues.
- **Tests/tooling explorer**: existing tests, type/lint setup, missing regression checks.
- **Caller-flow explorer**: call graph and shared-function impact; use only when many callers matter.
- **Lazy-dev explorer**: boilerplate, YAGNI, unnecessary abstractions, simpler stdlib/native alternatives.

## Prompt Template

```text
Review only this scope: <files/modules/request>.

Focus: <role-specific concern>.

Constraints:
- Read-only review. Do not edit files.
- Preserve project conventions.
- Separate correctness/maintainability risk from taste.
- Prefer the smallest safe change.
- Return only findings with file/line evidence, impact, and smallest fix.
- Say "no findings" if nothing material appears.
```

## Main-Agent Duties

After subagents return:

1. Merge duplicate findings.
2. Drop unsupported or taste-only claims unless labeled low impact.
3. Resolve conflicts using direct code evidence.
4. Include only findings you can defend.
5. Write the implementation plan from the final accepted findings.
