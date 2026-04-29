# Audit and Rate Limiting

## Audit Log Goals

External API access should be auditable because payment automation workflows can affect financial operations, support investigations, and security review. Audit logs should explain who called the API, which company scope was used, what operation was attempted, and what outcome occurred.

## What to Log

Recommended audit fields:

- Timestamp
- Request identifier
- Token identifier, not full token
- Resolved company identifier
- Endpoint or operation name
- Authentication result
- Authorization result
- Response status category
- Rate limit decision
- Error category
- Source IP or network metadata when appropriate
- Correlation identifier

## What Not to Log

Avoid logging:

- Full API keys
- Raw credentials
- Full payment payloads
- Customer personal data
- Bank account details
- Sensitive request bodies
- Internal secrets
- Stack traces in user-facing logs

If payload evidence is needed for support, use redaction, sampling, or restricted diagnostic records with retention controls.

## Rate Limiting Goals

Rate limiting protects platform reliability and reduces abuse risk. Limits should be predictable, documented, and applied before expensive downstream work.

Goals:

- Prevent accidental request floods.
- Reduce brute force token attempts.
- Protect shared infrastructure.
- Limit downstream integration pressure.
- Provide clear retry behavior.

## Per-Token and Per-Company Limits

Use both token and company-level limits where possible.

Per-token limits help isolate one integration credential. Per-company limits help prevent a company from bypassing controls by creating many tokens.

Example limit dimensions:

- Requests per minute per token
- Requests per hour per company
- Failed authentication attempts per source
- Expensive operation limits
- Background job or polling limits

## Alerting Scenarios

Alert when:

- Invalid token attempts spike.
- A revoked token is used repeatedly.
- A company exceeds normal usage patterns.
- A token suddenly becomes active after long inactivity.
- Rate limit violations persist.
- Sensitive endpoints see unusual traffic.
- Downstream integration errors increase.

## Abuse Detection

Abuse detection should combine rate signals, failure patterns, endpoint sensitivity, source network changes, and company usage history. The first response may be throttling or review rather than immediate blocking, depending on business risk.

## Deactivated or Expired Token Handling

Deactivated, expired, or revoked tokens should be rejected before application workflow execution. The response should avoid revealing whether the token was once valid.

Audit logs should record:

- Token identifier if it can be safely resolved
- Failure category
- Source metadata
- Endpoint
- Timestamp

## Operational Monitoring

Operational dashboards should track:

- Request volume by endpoint
- Request volume by company
- Authentication failures
- Authorization failures
- Rate limit rejections
- Downstream integration errors
- Latency percentiles
- Retry and polling patterns
- Token creation, rotation, and revocation activity
