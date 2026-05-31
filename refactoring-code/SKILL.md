---
name: refactoring-code
description: Refactors code to improve structure, readability, cohesion, and complexity without behavior changes. Use whenever the user asks to clean up or restructure code, even if they don't say skill.
---

# Refactoring Code

Use this skill when the user asks to clean up messy code, split a large function, reduce complexity, improve readability, remove duplication, or restructure code without changing behavior.

Make behavior preservation the center of the work. A refactor that changes contracts, state transitions, or user-visible output is a feature change unless the user explicitly asks for it.

## Workflow

1. Define the behavior boundary.
   Identify public APIs, inputs, outputs, side effects, database writes, events, errors, and tests that must remain stable.

2. Find the dominant smell.
   Choose the main structural problem before editing: mixed responsibilities, low cohesion, high coupling, duplicated logic, hidden side effects, unclear naming, or oversized control flow.

3. Pick the smallest refactor pattern that fits.
   Prefer extract function, extract module, move logic closer to ownership, rename for intent, remove duplication, introduce a small interface, or split orchestration from business rules. Use larger patterns only when the current shape demands them.

4. Plan the move sequence.
   Refactor in small steps that can be verified independently. Keep public signatures stable unless the user approves a contract change.

5. Execute and verify.
   Run the relevant formatter, typecheck, tests, or focused runtime checks. If verification is unavailable, say exactly what was not run.

6. Leave a narrow result.
   Avoid unrelated cleanup. The best refactor reduces cognitive load in the requested area without surprising neighboring code.

## Evidence Discipline

- Cite the files, symbols, tests, and behavior boundaries used to guide the refactor.
- Mark anything you cannot confirm as **unconfirmed** and explain what evidence would confirm it.
- Do not claim behavior is preserved unless you ran or inspected relevant verification.
- If the safe refactor requires a behavior change, stop and name that boundary before proceeding.

## Output Format

Use this structure:

```markdown
### Refactoring Strategy
- **Goal**: <structural improvement>
- **Behavior Boundary**: <what must not change>
- **Primary Smell**: <mixed responsibility, duplication, coupling, etc.>
- **Pattern**: <extract function/module, move class, adapter, etc.>

### Change Plan
1. <small move>
2. <small move>
3. <verification step>

### Refactored Result
<Patch summary or code excerpt, depending on the task.>

### Verification
- <commands/tests/checks run>
- <checks not run and why>

### Residual Risk
- <remaining complexity, trade-offs, or follow-up work>
```

Part of CDLI Agent Skills by CDLI - https://cdli.ai
