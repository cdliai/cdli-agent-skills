---
name: auditing-tech-debt
description: Audits codebases for duplication, dead code, drift, inconsistency, naming decay, complexity, and high-interest debt. Use whenever the user asks to find tech debt, even if they don't say skill.
---

# Auditing Tech Debt

Use this skill when the user asks for a technical debt audit, code smell scan, drift analysis, dead-code review, duplication review, maintainability review, or cleanup prioritization.

Treat technical debt as cost over time, not aesthetic discomfort. Rank debt by interest rate: how often the code changes, how many workflows it blocks, and how risky it is to keep touching.

## Workflow

1. Identify the system slice.
   Bound the audit to the module, folder, subsystem, or PR in front of you. Do not turn a targeted review into a repo-wide cleanup unless asked.

2. Collect evidence of interest rate.
   Use available signals: recent commits, call sites, test coverage, bug reports, repeated edits, ownership boundaries, and shared abstractions. If history is unavailable, mark interest-rate claims as **unconfirmed**.

3. Find debt categories.
   Look for duplication, drift between parallel implementations, dead or orphaned code, inconsistent naming, oversized functions, unclear ownership, missing tests around volatile code, stale dependencies, leaky abstractions, and configuration sprawl.

4. Classify the debt quadrant.
   Mark each item as prudent or reckless, deliberate or inadvertent. This separates acceptable trade-offs from accidental decay.

5. Prioritize by payoff.
   Put high-interest, low-cost fixes first. Defer low-interest cleanup unless it blocks current work or creates recurring mistakes.

6. Propose bounded remediation.
   Recommend small, verifiable steps. Avoid broad rewrites when a local consolidation, deleted dead path, or test addition would address the debt.

## Evidence Discipline

- Cite file paths, symbols, imports, routes, tests, or commit signals for every debt item.
- Mark anything you cannot confirm as **unconfirmed** and explain what evidence would confirm it.
- Do not call code dead until you have checked imports, route registration, exports, dynamic references, tests, jobs, and docs that may reference it.
- Distinguish "ugly but stable" from "expensive because it is frequently changed."

## Output Format

Use this structure:

```markdown
### Debt Summary
- **Scope**: <module, folder, subsystem, or repo slice>
- **Overall Interest Rate**: Low | Medium | High
- **Main Risk**: <why this debt matters>

### Debt Register
| Priority | Module | Debt Type | Evidence | Interest Rate | Quadrant | Remediation Cost |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| P1 | `<module>` | <duplication/drift/dead code/etc.> | `<file-or-symbol>` | High | Reckless/Inadvertent | <estimate> |

### Action Plan
1. **Quick Win**: <smallest high-payoff fix>
2. **Stabilizer**: <test, boundary, or ownership fix>
3. **Strategic**: <larger refactor or migration only if justified>

### Business Case
<One paragraph translating the debt into engineering time, release risk, onboarding cost, or defect risk.>

### Unconfirmed Areas
- <Claims that need history, coverage, runtime traces, or owner input.>
```

Part of CDLI Agent Skills by CDLI - https://cdli.ai
