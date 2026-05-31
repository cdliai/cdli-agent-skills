---
name: auditing-security
description: Audits code and configs for vulnerabilities, injection, auth, secrets, OWASP risks, and exposed surfaces. Use whenever the user asks to review, audit, or harden security, even if they don't say skill.
---

# Auditing Security

Use this skill when the user asks for a security audit, hardening pass, threat model, OWASP review, auth review, secret scan, or exposed-surface review.

Keep the work defensive. Identify vulnerabilities and safe remediation paths; do not provide weaponized exploit steps, harmful payloads, or instructions for abuse.

## Workflow

1. Map the attack surface.
   Identify every place untrusted input can enter: HTTP bodies, query strings, headers, cookies, file uploads, webhooks, queues, cron inputs, CLI arguments, environment variables, config files, and third-party callbacks.

2. Trace trust boundaries.
   Follow input across authentication, authorization, tenant boundaries, validation, persistence, rendering, logs, analytics, and outbound calls. Security issues often appear where ownership changes.

3. Verify controls.
   Check for input validation, output encoding, parameterized queries, CSRF/CORS posture, rate limiting, replay protection, session handling, authorization checks, encryption in transit or at rest, secret management, and least privilege.

4. Classify concrete vulnerabilities.
   Prefer confirmed findings over broad warnings. Useful categories include injection, broken auth, broken access control, XSS, unsafe redirects, insecure deserialization, SSRF, dependency exposure, sensitive logging, and misconfigured storage.

5. Explain one safe attack scenario when it clarifies impact.
   Keep scenarios high-level and non-operational: show the business or user impact without giving exploit instructions.

6. Recommend the smallest effective remediation.
   Prefer changes that reduce exposed surface, centralize policy, or make unsafe states impossible.

## Evidence Discipline

- Cite file paths, line numbers, symbols, endpoints, config keys, or routes for every finding.
- Mark anything you cannot confirm as **unconfirmed** and explain what evidence would confirm it.
- Do not guess. If credentials, policies, infrastructure, or runtime config are not visible, state the missing context.
- Do not report generic OWASP categories unless the code or config shows a plausible local instance.

## Severity

- **Critical**: credential exposure, unauthenticated data access, remote code execution, tenant escape, or direct path to data loss.
- **High**: broken authorization, exploitable injection, sensitive data leakage, or unsafe public write path.
- **Medium**: missing defense-in-depth around exposed input, weak validation, risky defaults, or incomplete auditability.
- **Low**: hardening opportunity with limited exploitability.

## Output Format

Use this structure:

```markdown
### Security Report
| Severity | Vulnerability | Evidence | Impact | Remediation |
| :--- | :--- | :--- | :--- | :--- |
| High | <issue> | `<file-or-endpoint>` | <risk> | <fix> |

### Attack Surface
- **Inputs Reviewed**: <routes, forms, jobs, configs, integrations>
- **Trust Boundaries**: <auth, tenant, network, browser, storage, third party>

### Safe Attack Scenario
<One non-weaponized scenario that explains impact, or "None needed.">

### Remediation Plan
1. <Smallest blocking fix>
2. <Follow-up hardening>

### Unconfirmed Areas
- <Missing context, runtime settings, external policies, or infrastructure not inspected.>
```

Part of CDLI Agent Skills by CDLI - https://cdli.ai
