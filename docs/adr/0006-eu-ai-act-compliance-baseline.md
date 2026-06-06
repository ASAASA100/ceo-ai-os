# ADR-0006: EU AI Act Compliance Baseline and Remediation Plan

**Date:** 2026-06-06
**Status:** Accepted
**Deciders:** Ajit Anand (AAP)

---

## Context

The CEO AI OS Phase 3a monitoring stack includes `compliance_check.py`, which runs a 15-point EU AI Act checklist across 5 domains. On first run (2026-06-06), the system scored **7/15 (46.7%)** — below the 80% production go-live threshold.

The EU AI Act classifies AI systems by risk level. CEO AI OS, as a governance and decision-support system used by a consulting practice, is assessed as **limited risk** (transparency obligations apply) with potential **high-risk** classification if used to make employment or credit decisions.

## Decision

**Establish 80% compliance as the go-live gate. Address all 8 identified gaps before production launch.**

### Gap Remediation Plan

| Domain | Gap | Remediation | Owner | Target |
|--------|-----|-------------|-------|--------|
| Human Oversight | Human review required for high-risk decisions | Implement approval workflow for risk scores ≥7 | OT-007 sprint | 23 Jun 2026 |
| Human Oversight | Override capability exists | Add `/api/override` endpoint with audit log | OT-007 sprint | 23 Jun 2026 |
| Human Oversight | Training provided to staff | Document user guide + record completion | Ajit | 30 Jun 2026 |
| Data Protection | User consent mechanism | Add consent flag to API onboarding flow | Phase 2 | 15 Jul 2026 |
| Data Protection | Data deletion policy | Draft DSAR/deletion SOP and link from API docs | Phase 2 | 15 Jul 2026 |
| Accountability | Exception handling documented | Add exception taxonomy to API docs | Phase 2 | 15 Jul 2026 |
| Transparency | Limitations disclosed | Add `GET /api/limitations` endpoint + disclosure doc | OT-007 sprint | 23 Jun 2026 |
| Security | HTTPS/TLS configured | Obtain TLS cert, configure reverse proxy | Phase 2 | 15 Jul 2026 |

### Score Projection

- After OT-007 sprint (23 Jun): 11/15 = **73%** (4 gaps closed)
- After Phase 2 (15 Jul): 15/15 = **100%** (all gaps closed)

## Consequences

- **Positive:** Compliance is tracked, measurable, and time-bound
- **Positive:** Compliance score will be monitored in CI via ADR-0002 gate
- **Negative:** Full 100% compliance deferred to 15 Jul — go-live at 73% requires a risk acceptance sign-off
- **Risk acceptance:** Ajit Anand, AAP — limited-risk system, no high-risk decisions in MVP scope

## Related

- OT-023 (monitoring stack — compliance_check.py)
- OT-029 (Phase 2 ADRs batch)
- `C:\Users\ajit1\Documents\Organized Files\CEO-AI-OS-Specs\003-EU-AI-Act-Validation-Spec.md`
