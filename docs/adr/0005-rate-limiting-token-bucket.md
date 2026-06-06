# ADR-0005: Rate Limiting — Token Bucket Algorithm

**Date:** 2026-06-06
**Status:** Accepted — Approved by Ajit Anand 2026-06-06
**Deciders:** Ajit Anand (AAP)

---

## Context

The CEO AI OS API must be protected against abuse (excessive requests from a single client) and denial-of-service conditions. Rate limiting strategy options:

| Algorithm | Behaviour | Suited for |
|-----------|-----------|------------|
| Fixed Window | Hard reset every N seconds — burst risk at window boundary | Simple but exploitable |
| Sliding Window | Smooth distribution over time | More accurate, higher memory |
| Token Bucket | Tokens refill continuously; burst up to bucket capacity | Best UX + burst tolerance |
| Leaky Bucket | Enforces strict output rate | Streaming / bandwidth-limited APIs |

Token bucket is the industry standard for REST APIs (used by Stripe, GitHub, AWS) and aligns with the RFC 6585 `429 Too Many Requests` + `Retry-After` response pattern.

## Decision

**Implement token bucket rate limiting on all CEO AI OS API endpoints.**

Specification:
- Standard endpoints: 2,000 requests / minute per client
- Data/governance endpoints: 500 requests / minute per client
- Burst allowance: Up to 2× bucket capacity in a single burst
- Response on limit: `429 Too Many Requests` with `Retry-After` header
- Client identity: JWT `sub` claim (authenticated) or IP address (unauthenticated)
- Storage: In-memory for single-node; Redis for multi-node (Phase 2+)

Current `security.py` implements a 10 req/min dev variant — production limits apply at go-live.

## Consequences

- **Positive:** Prevents abuse without degrading legitimate usage patterns
- **Positive:** `Retry-After` header allows clients to back off gracefully
- **Negative:** In-memory storage lost on restart — acceptable for single-node MVP; Redis needed for HA
- **Implementation:** Wire `security.check_rate_limit()` into Flask middleware / ASGI middleware

## Related

- OT-022 (spec approved 2026-06-06)
- ADR-0004 (JWT auth — client identity source)
- `C:\Users\ajit1\Documents\Organized Files\CEO-AI-OS-Specs\002-Rate-Limiting-Token-Bucket-Spec.md`
