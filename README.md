# CDLI Agent Skills

CDLI Agent Skills is a small public collection of capability-first engineering skills by CDLI. It distills internal agent prompt patterns into portable, readable workflows for auditing, mapping, refactoring, and shipping software with evidence.

This is a visibility and craft collection, not a paid product. Each skill is intentionally narrow: it says what task should trigger it, how to perform that task, and what output shape to produce.

## Included Skills

- `reviewing-code`: review pull requests and diffs for merge risk, correctness, performance, and maintainability.
- `auditing-security`: audit exposed surfaces for vulnerabilities, auth flaws, secret handling, and unsafe data flow.
- `auditing-tech-debt`: find high-interest debt, duplication, drift, dead code, and inconsistent implementation patterns.
- `refactoring-code`: restructure code for readability and maintainability without changing behavior.
- `mapping-architecture`: diagram and explain a codebase or system before making architecture judgments.
- `reviewing-api-contracts`: review REST and GraphQL contracts for resource shape, auth, errors, versioning, and developer experience.

## Install

Clone the public repository, then copy the skill directories into the skills folder used by your agent runtime. Keep each `SKILL.md` with its parent directory name.

```bash
git clone https://github.com/cdliai/cdli-agent-skills.git
```

Claude Code personal skills:

```bash
mkdir -p ~/.claude/skills
cp -R cdli-agent-skills/*/ ~/.claude/skills/
```

Codex and other local agents:

```bash
mkdir -p ~/.codex/skills
cp -R cdli-agent-skills/*/ ~/.codex/skills/
```

Folder shape:

```text
skills/
  reviewing-code/
    SKILL.md
  auditing-security/
    SKILL.md
```

## Design Principles

- Convert personas into capabilities. A skill should trigger on a task, not an identity.
- Prefer evidence over assumption. Cite files, symbols, endpoints, or commands; mark anything unconfirmed.
- Keep reports consistent. A predictable output format makes findings easier to compare, share, and act on.
- Keep public skills portable. Do not include private endpoints, internal paths, secrets, or surprise side effects.

Part of CDLI Agent Skills by CDLI - https://cdli.ai
