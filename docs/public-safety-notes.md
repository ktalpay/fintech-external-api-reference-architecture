# Public Safety Notes

## What Was Intentionally Excluded

This artifact intentionally excludes:

- Private source code
- Employer names
- Product names
- Customer names
- Internal API URLs
- Internal database schemas
- Credentials or secrets
- Infrastructure identifiers
- Real logs
- Real payloads
- Transaction volume
- Revenue impact
- Customer counts
- Commercial claims

## How Confidential Details Are Avoided

The documents use generalized component names and reference architecture language. They describe common security and architecture patterns without copying internal implementation details, source code, schema names, operational data, or private system behavior.

The artifact is written as a reusable public architecture note, not as documentation for a real private platform.

## How to Write Sanitized Architecture Evidence

Use:

- General component names
- Public-safe diagrams
- Pattern descriptions
- Decision records
- Security assumptions
- Non-goals
- Example flows with fictional identifiers

Avoid:

- Internal names
- Customer examples
- Real payloads
- Real API paths if private
- Private database tables
- Commercial metrics
- Screenshots containing sensitive data
- Code copied from private repositories

## What Must Not Be Committed

Do not commit:

- `.env` files
- Access tokens
- API keys
- Private certificates
- Customer exports
- Internal logs
- Production configuration
- Private source code
- Database dumps
- Proprietary diagrams
- Screenshots with confidential data

## Secret Scanning and Repository Hygiene Checklist

- [ ] Run secret scanning before publishing.
- [ ] Review Git history before making the repository public.
- [ ] Confirm no private names appear in docs.
- [ ] Confirm diagrams use generic components.
- [ ] Confirm sample identifiers are fictional.
- [ ] Confirm no real URLs are included.
- [ ] Confirm no customer or employer names are included.
- [ ] Add a public-safe disclaimer in the README.
- [ ] Use a license only after checking publication intent.
- [ ] Keep evidence claims aligned with the evidence matrix.
