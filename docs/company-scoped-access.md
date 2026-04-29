# Company-Scoped Access

## Company Ownership Model

Each API key belongs to a single company or tenant. The API key is not only a secret; it is an ownership boundary. When a request arrives, the platform resolves the token to its owning company and uses that company as the authorization scope.

## Resolving CompanyId from API Key

When a request arrives with `X-Api-Key`, the API resolves the token to its owning `CompanyId` and scopes all returned data to that company.

For example, if the token belongs to `CompanyId 12` and the request asks for a bank list, only banks associated with `CompanyId 12` should be returned.

## Do Not Trust User-Supplied CompanyId

The client should not be trusted to provide its own company authorization scope. A request body, query string, or route parameter containing `CompanyId` should not override the company resolved from the API key.

Unsafe pattern:

```text
GET /banks?companyId=42
X-Api-Key: token-owned-by-company-12
```

The API must not return `CompanyId 42` data just because the request asked for it.

Safe pattern:

```text
GET /banks
X-Api-Key: token-owned-by-company-12
```

The API resolves the token owner and returns only company 12 data.

## Ensuring Returned Data Is Scoped

Data access should apply the resolved company scope at the application or repository boundary. The scope should be part of the query model, not a filter added manually in scattered controller code.

Recommended controls:

- Resolve company scope once per request.
- Pass company scope through application commands and queries.
- Apply company scope in all reads and writes.
- Reject cross-company resource access.
- Test that data from other companies cannot be returned.

## Example Safe Request Flow

1. Client sends request with `X-Api-Key`.
2. API validates and hashes the token.
3. Token lookup returns `CompanyId 12`.
4. Request context is created with `CompanyId 12`.
5. Application query asks for banks within `CompanyId 12`.
6. Data layer returns only records owned by `CompanyId 12`.
7. Audit log records token identity, company scope, endpoint, and result status.

## Common Failure Cases

- Missing API key
- Token maps to inactive company
- Token maps to revoked company access
- Request asks for another company resource
- Company scope is not applied to a query
- Background job loses company context
- Audit log does not include resolved company

## Security Test Cases

- A token for company 12 cannot read company 13 banks.
- A token for company 12 cannot create records under company 13.
- A request body `CompanyId` cannot override token ownership.
- A route parameter cannot bypass company scope.
- Revoked tokens cannot access any company data.
- Expired tokens cannot access company data.
- Audit logs include resolved company scope.
- Error responses do not reveal other company identifiers.

## Architectural Note

The most important design choice in this document is not the use of an API key itself. The important part is what the API key resolves to.

If the token only answers “is this caller authenticated?”, the API still needs a separate and reliable authorization boundary. In this model, the token resolves to an owning company, and that company becomes the default scope for all downstream commands and queries.

This reduces the risk of cross-company access caused by trusting request parameters, route values, or client-side assumptions.
