# ADR-001: API Key Authentication for External Integrations

## Status

Proposed

## Context

External system-to-system integrations often need a stable authentication mechanism for controlled API access. In a FinTech payment automation context, the authentication mechanism must support ownership, revocation, auditability, and operational monitoring.

This reference architecture uses API key authentication as a baseline pattern for external integrations. It is not presented as the only valid option or as a complete security model by itself.

## Decision

Use API key authentication for the initial external integration model. Tokens are generated with high entropy, shown once to the client, stored only as hashes, and linked to ownership metadata such as company, status, expiry, and optional scopes.

Requests include the token in `X-Api-Key`. The API hashes the submitted token, validates token status, resolves ownership metadata, and applies company-scoped access before executing application logic.

## Consequences

- The authentication flow remains simple for external clients.
- Tokens can be revoked, rotated, and audited.
- Token storage must be treated as security-sensitive.
- API keys must be combined with rate limiting, audit logs, and company scoping.
- Future migration to scoped tokens or OAuth should remain possible.

## Alternatives Considered

- OAuth 2.0 client credentials: stronger standards alignment, but more operational complexity for early controlled integrations.
- Mutual TLS: strong client authentication, but higher certificate and infrastructure overhead.
- Signed requests: useful for replay resistance, but more complex for partner implementation.
- Basic authentication: rejected because it does not provide a strong lifecycle model for integration credentials.
