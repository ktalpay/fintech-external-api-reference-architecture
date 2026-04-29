# API Key Authentication

## Why API Key Authentication May Be Used

API key authentication can be appropriate for controlled external integrations where a partner or system-to-system client needs stable access to a limited API surface. It is simple to operate, easy to rotate, and can be combined with company ownership, scopes, rate limits, and audit logging.

API keys should not be treated as a complete security model by themselves. They need lifecycle management, secure storage, revocation, monitoring, and clear access boundaries.

## Token Generation Model

A safe token generation model should:

- Generate high-entropy random tokens.
- Show the full token only once at creation time.
- Store metadata such as owner company, status, creation time, expiry, and last-used time.
- Store only a hash of the token.
- Support explicit rotation and revocation.

## Token Hashing

API keys should be stored as hashes, not plaintext secrets. A request token is hashed and compared against stored token hashes. The full token should not appear in logs, database rows, error messages, screenshots, or support tools.

Useful metadata can be stored separately from the secret:

- Token identifier
- Owning company identifier
- Status
- Created timestamp
- Expiry timestamp
- Last used timestamp
- Optional scope list

## Secure Storage

Token records should be protected as security-sensitive data. Access should be limited to backend services and operational users with a clear support need. Administrative tooling should avoid showing full tokens after creation.

## Rotation and Revocation

Token lifecycle controls should include:

- Create new token
- Activate token
- Deactivate token
- Revoke compromised token
- Set expiry date
- Track last used date
- Notify owner before expiry if appropriate

Rotation should allow a transition period when the old and new token can both be active, if the risk model allows it.

## Request Authentication Flow

1. Client sends `X-Api-Key`.
2. API checks that the header exists.
3. API hashes the submitted token.
4. API searches for an active matching token hash.
5. API rejects expired, revoked, or inactive tokens.
6. API resolves token ownership metadata.
7. API applies company scope and optional permissions.
8. API records authentication result in audit logs.

## Failure Handling

Authentication failures should be consistent and non-revealing. Error responses should not confirm whether a token exists, whether a company exists, or which part of the credential failed.

Common failure cases:

- Missing API key
- Invalid API key
- Expired token
- Revoked token
- Inactive token
- Token without required permissions
- Excessive failed attempts

## Abuse Detection Considerations

Signals to monitor:

- Repeated invalid token attempts
- Unusual request spikes
- Repeated access to unauthorized resources
- Requests from unexpected network ranges
- High failure rates
- Sudden usage after long inactivity

Abuse detection should feed alerting, temporary throttling, or token review workflows.

## Future Migration Path

API key authentication can be extended or replaced over time with:

- Scoped tokens
- OAuth 2.0 client credentials
- Mutual TLS
- Signed requests
- Per-endpoint permissions
- Short-lived access tokens

The reference architecture keeps token ownership and company scoping separate so a future authentication mechanism can reuse the same authorization model.
