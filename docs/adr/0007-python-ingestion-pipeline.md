# ADR-0007: Python Ingestion Pipeline — Phase 2

**Date:** 2026-06-06
**Status:** Accepted
**Deciders:** Ajit Anand (AAP)

---

## Context

The CEO AI OS Second Brain (28-folder PARA/CODE/ICOR structure) currently relies on manual ingestion — files are saved to the correct folder by the user or by individual skill outputs. There is no automated pipeline to ingest content from external sources (email, calendar, webinars, documents) into the Second Brain in a normalised, queryable format.

A Python ingestion pipeline was proposed in Phase 2 planning. The prerequisite is a stable monitoring baseline (ADR-0001) to size the pipeline correctly.

## Decision

**Build a Python Ingestion Pipeline in Phase 2, targeting 15 Jul 2026.**

Design decisions:
- **Language:** Python 3.14 (consistent with deployment venv)
- **Trigger:** Scheduled via Windows Task Scheduler (daily, 06:00) or on-demand via Dispatcher webhook
- **Sources (Phase 2 scope):** Yahoo Mail (IMAP), iCloud Calendar (CalDAV), YouTube/webinar URLs
- **Output format:** Markdown files with YAML frontmatter (`title`, `source`, `date`, `tags`, `icor_layer`)
- **Destination:** CEO AI OS Second Brain — routed to correct folder by content classifier
- **Deduplication:** SHA-256 hash of source URL + date; skip if already ingested
- **Error handling:** Failed ingestions logged to `ingestion_errors.jsonl`; no silent failures

## Consequences

- **Positive:** Reduces manual knowledge capture to near-zero for supported source types
- **Positive:** Consistent YAML frontmatter enables future RAG/search layer
- **Negative:** Requires Second Brain root path to be stable (currently `C:\Users\ajit1\Documents\28 Folders\`)
- **Dependency:** ADR-0001 monitoring baseline must be established first
- **Watch point:** iCloud CalDAV session renewal (iCloud app password rotates) — handle 401 gracefully

## Related

- OT-029 (Phase 2 ADRs batch — due 15 Jul 2026)
- ADR-0001 (Automated Ingestion Thresholds — prerequisite)
- `reference_video_analysis_skill.md` (Second Brain routing design)
- Second Brain root: `C:\Users\ajit1\Documents\28 Folders\`
