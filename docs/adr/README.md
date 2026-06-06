# Architecture Decision Records (ADRs)

CEO AI OS architectural decisions, captured in [Michael Nygard format](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions).

## Index

| ADR | Title | Status | Date |
|-----|-------|--------|------|
| [ADR-0001](0001-automated-ingestion-thresholds.md) | Defer Automated Ingestion Thresholds to Phase 2 | Accepted | 2026-06-06 |
| [ADR-0002](0002-cicd-regression-testing.md) | CI/CD Regression Testing Gate | Accepted | 2026-06-06 |
| [ADR-0003](0003-multi-agent-orchestration.md) | Multi-Agent Orchestration as MVP Core | Accepted | 2026-06-06 |
| [ADR-0004](0004-jwt-authentication-rs256.md) | JWT Authentication RS256 | Accepted | 2026-06-06 |
| [ADR-0005](0005-rate-limiting-token-bucket.md) | Rate Limiting — Token Bucket Algorithm | Accepted | 2026-06-06 |
| [ADR-0006](0006-eu-ai-act-compliance-baseline.md) | EU AI Act Compliance Baseline and Remediation Plan | Accepted | 2026-06-06 |
| [ADR-0007](0007-python-ingestion-pipeline.md) | Python Ingestion Pipeline — Phase 2 | Accepted | 2026-06-06 |

## How to add an ADR

1. Copy the template below
2. Name the file `NNNN-short-title.md` (next sequential number)
3. Add a row to the index above
4. Submit via PR or commit directly to `master`

## Template

```markdown
# ADR-NNNN: Title

**Date:** YYYY-MM-DD
**Status:** Proposed | Accepted | Deprecated | Superseded by ADR-XXXX
**Deciders:** Name (Role)

---

## Context
## Decision
## Consequences
## Related
```
