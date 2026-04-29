# Publication Checklist

## Before Making the Repository Public

- [ ] Run confidentiality scan.
- [ ] Run product, employer, customer, and private system name scan.
- [ ] Run secret scan.
- [ ] Validate all relative links.
- [ ] Check Mermaid diagram rendering.
- [ ] Review README clarity.
- [ ] Review evidence language.
- [ ] Confirm license decision.
- [ ] Add GitHub topics.
- [ ] Capture repository screenshots.
- [ ] Update evidence matrix after public URL exists.
- [ ] Prepare LinkedIn post.
- [ ] Update GitHub profile README link.
- [ ] Decide whether the repo is ready to pin.

## Confidentiality Scan

- [ ] No employer names.
- [ ] No product names.
- [ ] No customer names.
- [ ] No private system names.
- [ ] No real internal API URLs.
- [ ] No private database schemas.
- [ ] No real logs or payloads.

## Secret Scan

- [ ] No API keys.
- [ ] No tokens.
- [ ] No passwords.
- [ ] No private certificates.
- [ ] No `.env` files.
- [ ] No cloud credentials.
- [ ] No internal configuration files.

## Evidence Language Check

- [ ] Uses "reference architecture" wording.
- [ ] Uses "sanitized artifact" wording where appropriate.
- [ ] Uses "evidence candidate" wording.
- [ ] Does not claim public adoption.
- [ ] Does not claim commercial impact.
- [ ] Does not imply production ownership by itself.
- [ ] Does not sound like a direct internal implementation.

## Do Not Publish If

- Any employer, product, customer, or private system name appears.
- Any real endpoint or private schema appears.
- Any secret or token appears.
- Any commercial metric is unsupported.
- The artifact sounds like production code or direct internal implementation.
- Mermaid or document links are broken.
- License decision is unresolved.
- Evidence wording overclaims the artifact's value.
