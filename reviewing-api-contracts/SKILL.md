---
name: reviewing-api-contracts
description: Reviews REST or GraphQL API contracts for endpoints, schemas, versioning, auth, errors, and DX. Use whenever the user asks to design or review API shape, even if they don't say skill.
---

# Reviewing API Contracts

Use this skill when the user asks to design, review, or harden a REST or GraphQL API contract, endpoint shape, request/response schema, auth model, versioning approach, or frontend/backend contract.

Stay at the contract layer. Define or review the interface, security model, data flow, and error semantics; do not drift into controller implementation unless the user asks for code.

## Workflow

1. Recover the resource model.
   Name the nouns being manipulated, their parent resources, ownership boundaries, lifecycle states, and relationships. Prefer resource names over action-shaped endpoints.

2. Check operation semantics.
   For REST, verify method choice, idempotency, status codes, pagination, filtering, sorting, cache behavior, file upload strategy, and versioning. For GraphQL, verify schema shape, nullability, mutations, pagination, field-level auth, and N+1 risk.

3. Define request and response contracts.
   Make required fields, optional fields, defaults, validation rules, enums, timestamps, IDs, and error envelopes explicit.

4. Review security by design.
   Check authentication, authorization, scopes or roles, tenant isolation, rate limits, replay protection, input limits, and sensitive-field exposure.

5. Review compatibility and developer experience.
   Look for backward compatibility, consistent naming, predictable error shapes, useful examples, discoverability, and migration paths.

6. Recommend contract changes before implementation details.
   The API contract should make unsafe or inconsistent implementation harder.

## Evidence Discipline

- Cite endpoint paths, schema fields, resolver names, OpenAPI sections, route files, or frontend call sites for every finding.
- Mark anything you cannot confirm as **unconfirmed** and explain what evidence would confirm it.
- Do not assume auth, tenancy, rate limits, or storage behavior if the contract does not state it.
- Separate contract defects from implementation defects.

## Output Format

Use this structure:

````markdown
### API Contract Verdict
- **Scope**: <endpoint, resource, schema, or feature>
- **Status**: Accept | Revise | Block
- **Primary Risk**: <contract risk>

### Resource Model
- **Resource**: <noun>
- **Parent/Owner**: <parent resource or principal>
- **Lifecycle**: <states if relevant>

### Contract Findings
| Severity | Area | Evidence | Issue | Recommendation |
| :--- | :--- | :--- | :--- | :--- |
| High | AuthZ | `<endpoint-or-field>` | <problem> | <fix> |

### Proposed Contract
Use REST/OpenAPI-style YAML for REST endpoints, or GraphQL SDL for GraphQL contracts.

```yaml
method: PUT
path: /v1/resources/{resourceId}
auth:
  scheme: Bearer
  scopes: [resource:write]
request:
  contentType: application/json
  body: {}
responses:
  200: {}
  400: { error: { code: string, message: string } }
```

### Security and Performance Notes
- <auth, rate limit, payload limit, caching, or pagination note>

### Compatibility Notes
- <versioning, migration, deprecation, or client impact>

### Unconfirmed Areas
- <missing requirements, auth policy, infra limits, or caller behavior>
````

Part of CDLI Agent Skills by CDLI - https://cdli.ai
