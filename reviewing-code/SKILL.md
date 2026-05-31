---
name: reviewing-code
description: Reviews pull requests and diffs for correctness, logic errors, performance, style, and merge risk. Use whenever the user asks to review code before merge, even if they don't say skill.
---

# Reviewing Code

Use this skill when the user asks for a code review, pull request review, diff review, merge readiness check, or pre-merge quality gate.

Do not spend review budget on formatting that an automated formatter would fix. Prioritize issues that can break behavior, weaken security, create production risk, or make the code harder to maintain.

## Workflow

1. Recover the intent of the change.
   Read the diff, touched files, nearby call sites, and tests before judging the code. A review without intent tends to become style commentary.

2. Check correctness first.
   Look for logic errors, off-by-one conditions, bad null handling, race conditions, broken state transitions, missing error handling, and mismatches between names and behavior.

3. Check merge risk.
   Look for public API changes, database or schema changes, migrations, config changes, feature flags, background jobs, and dependency changes that may affect callers outside the diff.

4. Check security and data handling.
   Flag only concrete risks in the reviewed surface: injection, unsafe deserialization, missing authorization, secret exposure, unsafe logging, weak validation, or privacy leaks.

5. Check performance where behavior suggests risk.
   Look for accidental N+1 queries, sequential awaits that should be parallel, repeated expensive work, unbounded loops, blocking I/O, and unnecessary re-renders.

6. Check tests and verification.
   Ask whether the change has tests at the right level. Prefer focused tests for logic changes, integration tests for contract changes, and regression tests for bug fixes.

## Evidence Discipline

- Cite file paths, line numbers, symbols, endpoints, or test names for every finding.
- Mark anything you cannot confirm as **unconfirmed** and explain what evidence would confirm it.
- Do not guess. If the surrounding context is missing, say what is missing and limit the claim.
- Separate must-fix findings from optional improvements.

## Severity

- **Critical**: likely security breach, data loss, outage, or irreversible corruption.
- **High**: likely user-facing breakage, authorization failure, severe performance regression, or broken contract.
- **Medium**: correctness risk in edge cases, maintainability issue with clear future cost, or missing tests around risky logic.
- **Low**: localized improvement with limited behavioral risk.

## Output Format

Use this structure:

```markdown
### Review Summary
- **Status**: Approve | Comment | Request Changes | Reject
- **Risk Level**: Low | Medium | High | Critical
- **Scope Reviewed**: <diff, files, PR, or modules reviewed>

### Findings
1. **[Severity] <finding title>**
   - **Evidence**: `<file-or-symbol>` and the relevant observed behavior.
   - **Impact**: What can break or degrade.
   - **Recommendation**: The smallest practical fix.

### Required Changes
- <Blocking changes before merge, or "None.">

### Improvements
- <Non-blocking follow-ups, or "None.">

### Verification Gaps
- <Tests, commands, or runtime checks that were missing or not run.>
```

Part of CDLI Agent Skills by CDLI - https://cdli.ai
