# ADR-0001: Defer Automated Ingestion Thresholds to Phase 2

**Date:** 2026-06-06
**Status:** Accepted
**Deciders:** Ajit Anand (AAP)

---

## Context

The CEO AI OS monitoring stack (Phase 3a) includes observability modules for governance workflows, Prometheus metrics, and audit logging. A recommendation was raised to implement automated ingestion thresholds — rules that would auto-trigger data ingestion pipelines when metric thresholds are breached.

Threshold configuration requires a stable baseline of real operational data to be meaningful. Without it, thresholds would be arbitrary and generate false positives or miss genuine spikes.

## Decision

**Defer Automated Ingestion Thresholds to Phase 2.**

Thresholds will not be implemented until:
1. The monitoring stack (OT-023) is fully deployed
2. At least two weeks of baseline metric data is collected via Prometheus
3. Mean/P95 values are established for `governance_assessments_total` and `assessment_duration_seconds`

## Consequences

- **Positive:** Avoids premature configuration; threshold values will be evidence-based
- **Positive:** Reduces Phase 1 scope, accelerating go-live
- **Negative:** Ingestion remains manual/scheduled until Phase 2 lands
- **Trigger:** Revisit this ADR after `Day3_Monitoring_Tests.bat` has run in production for 14+ days

## Related

- OT-023 (monitoring stack deployment)
- ADR-0007 (Python Ingestion Phase 2)
