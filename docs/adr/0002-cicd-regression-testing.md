# ADR-0002: CI/CD Regression Testing Gate

**Date:** 2026-06-06
**Status:** Accepted
**Deciders:** Ajit Anand (AAP)

---

## Context

CEO AI OS Phase 3a introduced five new Python modules (`monitoring_config.py`, `metrics.py`, `security.py`, `audit_logging.py`, `compliance_check.py`) and a test harness (`Day3_Monitoring_Tests.bat`). As the system grows, manual test execution is not sustainable. A CI/CD regression gate is needed to catch regressions before they reach production.

The current sprint (OT-007, due 23 Jun 2026) is the active priority. A CI/CD pipeline requires a stable deployment structure, which OT-007 is still establishing.

## Decision

**Implement a CI/CD regression testing gate in Phase 2, targeting completion by 10 Jun 2026 (OT-029).**

The gate will:
1. Run `Day3_Monitoring_Tests.bat` (or equivalent Python test runner) on every push to `master`
2. Block merge if any module test fails
3. Report compliance score from `compliance_check.py` as a PR check
4. Use GitHub Actions as the CI provider (no additional tooling required for this repo)

## Consequences

- **Positive:** Prevents regressions in monitoring stack as codebase grows
- **Positive:** Compliance score tracked over time via CI run history
- **Negative:** Small overhead per push; mitigated by fast test suite (~5 seconds)
- **Implementation note:** GitHub Actions workflow file: `.github/workflows/test.yml`

## Related

- OT-007 (CEO AI OS MVP sprint)
- OT-029 (Phase 2 ADRs batch)
- ADR-0001 (monitoring stack)
