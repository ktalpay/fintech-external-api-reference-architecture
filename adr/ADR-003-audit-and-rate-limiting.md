# ADR-003: Audit Logging and Rate Limiting as Baseline External API Controls

## Status

Proposed

## Context

External APIs in FinTech-style payment automation workflows need operational visibility and abuse controls. Authentication alone does not explain what happened, support investigations, or protect the platform from excessive or unusual usage.

## Decision

Use audit logging and rate limiting as baseline controls for all external API access. Audit logs record token identity, resolved company scope, endpoint, result status, and security-relevant decisions without storing secrets or sensitive payloads. Rate limiting is applied per token and per company before expensive application workflows execute.

## Consequences

- Security and support teams can investigate access patterns.
- Excessive usage can be throttled before it affects downstream services.
- Audit data must be designed with privacy and retention controls.
- Sensitive payloads and credentials must not be logged.
- Rate limit thresholds need operational review and tuning.

## Alternatives Considered

- Audit logging only on failures: rejected because successful operations also matter for traceability.
- Global rate limits only: rejected because they do not isolate token or company behavior.
- Downstream-only throttling: rejected because expensive work may already have happened.
- Full payload logging: rejected because it creates privacy and security risk.
