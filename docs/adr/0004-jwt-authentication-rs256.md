# ADR-0004: JWT Authentication RS256

**Date:** 2026-06-06
**Status:** Accepted — Approved by Ajit Anand 2026-06-06
**Deciders:** Ajit Anand (AAP)

---

## Context

The CEO AI OS API layer requires a token-based authentication mechanism. Options evaluated:

| Option | Pros | Cons |
|--------|------|------|
| HS256 (symmetric) | Simple, fast | Shared secret — key compromise affects all services |
| RS256 (asymmetric) | Private key signs, public key verifies; key rotation per service | Slightly more complex setup |
| API Key (static) | Trivial to implement | No expiry, difficult to rotate, no claims |

The system will eventually expose APIs to external clients and mobile (iPhone Dispatcher). Asymmetric signing allows public key distribution without exposing the signing secret.

## Decision

**Use RS256 (RSA asymmetric) JWT for all CEO AI OS API authentication.**

Specification:
- Algorithm: RS256
- Access token TTL: 15 minutes
- Refresh token TTL: 7 days (httpOnly cookie, not in localStorage)
- Key rotation: Quarterly (calendar reminder)
- Claims: `sub` (user ID), `role`, `exp`, `iat`
- Key storage: Private key in `.env` / environment variable; public key exposed at `/.well-known/jwks.json`

Note: Current `security.py` uses HS256 for local dev. RS256 implementation targets Phase 2 go-live.

## Consequences

- **Positive:** Each microservice can verify tokens without access to private key
- **Positive:** Quarterly key rotation limits blast radius of compromise
- **Negative:** Requires key pair generation and JWKS endpoint before go-live
- **Migration:** Update `security.py` → replace `HS256` with `RS256`, wire private key from env

## Related

- OT-022 (spec approved 2026-06-06)
- ADR-0005 (rate limiting)
- `C:\Users\ajit1\Documents\Organized Files\CEO-AI-OS-Specs\001-JWT-Authentication-Spec.md`
