# ADR-002: Company-Scoped Data Access Resolved from API Key Ownership

## Status

Proposed

## Context

External API clients must only access data owned by their company or tenant. A common failure mode is trusting caller-supplied company identifiers in query strings, routes, or request bodies. That can create cross-company access risk if authorization boundaries are not enforced centrally.

## Decision

Resolve the owning company from the submitted API key and use that resolved company as the authorization scope for all reads and writes. Caller-supplied company identifiers must not override token ownership.

For example, if a token belongs to `CompanyId 12`, a request for a bank list returns only banks associated with `CompanyId 12`.

## Consequences

- Company boundaries are enforced consistently.
- The API key becomes both a credential and an ownership boundary.
- Application services must carry company scope through commands and queries.
- Tests must verify that cross-company access is rejected.
- Background processing must preserve company context.

## Alternatives Considered

- Trusting `CompanyId` from request parameters: rejected because it creates cross-company access risk.
- Per-company API base URLs: possible, but operationally heavier and still requires backend authorization.
- User-based authentication only: useful for user workflows, but not sufficient for system-to-system external integrations.
- Endpoint-specific company filters: rejected as the primary model because scattered filtering is easy to miss.

This decision intentionally puts company-scope resolution close to authentication rather than leaving it to individual endpoints. The trade-off is that application services must consistently carry scope context, but the benefit is a clearer and more testable authorization boundary.
