# Output Format

Keep reviews direct and decision-oriented.

## Default Shape

Start with the main recommendation:

```text
Main call: <keep simple | small refactor | introduce class | introduce Pydantic model/settings | larger design issue>
Why: <one or two concrete reasons>
```

Then list findings by impact:

```text
Findings:
- High: <issue, location, smallest fix>
- Medium: <issue, location, smallest fix>
- Low: <taste-only or cleanup>
```

Include code only when it makes the recommendation clearer.

## After Review

After the review findings, always write a short implementation plan for the recommended changes before asking for action:

```text
Recommended implementation plan:
1. <smallest concrete change>
2. <next concrete change, if needed>
```

Then ask the user whether to implement that plan, verify it first, or change parts of it.

If the user wants to change the plan, ask whether they have specific edits, want a different recommendation, or want to brainstorm alternatives.

If the user wants to brainstorm, invoke `superpowers:brainstorming` before revising the plan.

## Questions

Never ask bulk question lists.

If blocked, ask one targeted question. If not blocked, proceed with a reasonable assumption and state it.

When choices are useful, present options:

```text
Options:
1. Keep functions. Best if <condition>.
2. Introduce `XService`. Recommended because <reason>.
3. Split model/settings first. Best if <condition>.
```

Always mark the recommended option unless the facts are genuinely missing.

## Tone

Separate evidence from preference. Say when something is taste, project convention, or concrete maintainability risk.

Do not equate "Pythonic" with "more classes." In this skill, the preference is OOP for maintainability, but only when the code benefits from ownership, state, lifecycle, polymorphism, or dependency boundaries.
