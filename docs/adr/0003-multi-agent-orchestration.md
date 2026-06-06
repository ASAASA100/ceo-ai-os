# ADR-0003: Multi-Agent Orchestration as MVP Core

**Date:** 2026-06-06
**Status:** Accepted
**Deciders:** Ajit Anand (AAP)

---

## Context

Three architectural patterns were evaluated for the CEO AI OS Phase 2 build: Automated Ingestion Thresholds, CI/CD Regression Testing, and Multi-Agent Orchestration. A question arose whether Multi-Agent Orchestration should be deferred to a later phase or treated as an immediate build priority.

The CEO AI OS is fundamentally a multi-agent system. Layer 3 (Orchestration) — the component that routes tasks across specialist agents (Chief of Staff, Director AI/ML, PMO, etc.) — is the core value proposition, not an enhancement.

## Decision

**Multi-Agent Orchestration is in scope for the current MVP sprint (OT-007, due 23 Jun 2026).** It is not deferred.

Layer 3 architecture:
- **Dispatcher** (already live): webhook server routing commands to PS1 scripts
- **Specialist agents**: invoked via Claude CLI or direct Python scripts
- **Orchestration pattern**: Sequential agent handoff with shared context via `context-state.md`
- **Agentic patterns framework**: Formal design spec applied to all new agents (see `agentic-patterns` skill)

## Consequences

- **Positive:** Multi-agent capability available at MVP go-live (23 Jun 2026)
- **Positive:** Dispatcher + scheduling infrastructure already proven in production
- **Negative:** Higher MVP complexity; mitigated by existing dispatcher scaffolding
- **Watch point:** Agent handoff reliability — monitor via `dispatcher.log` for command timeouts

## Related

- OT-007 (MVP sprint)
- OT-024 (Dispatcher scheduled task — Done)
- OT-025 (Flagged email fix — Done)
