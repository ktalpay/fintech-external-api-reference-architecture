# GitHub Publication Steps

## Target Repository

Repository name:

`fintech-external-api-reference-architecture`

Description:

`Public-safe reference architecture for secure external API access in FinTech payment automation platforms.`

Visibility:

Public, only after final checklist passes.

License:

Apache-2.0, unless final human review decides to delay licensing.

## Pre-Publication Gates

- QA report reviewed
- Confidentiality scan clean
- Secret scan clean
- Relative links valid
- Mermaid syntax checked
- Final human confidentiality review completed
- License decision completed

## Option A: GitHub CLI Flow

Assumptions:

- GitHub username: `ktalpay`
- Local artifact directory: `/Users/kursatalpay/Documents/gtv/projects/fintech-external-api-reference-architecture`
- Repository name: `fintech-external-api-reference-architecture`

Run each command only after confirming the previous step is correct. Skip commands that are already done.

```bash
cd /Users/kursatalpay/Documents/gtv/projects/fintech-external-api-reference-architecture
```

Check whether git is already initialized:

```bash
git status
```

If this is not a git repository, initialize it:

```bash
git init
```

Add a `.gitignore` if needed. Keep it minimal for a documentation repository:

```bash
printf ".DS_Store\n.env\n*.log\n" > .gitignore
```

If Apache-2.0 is selected, add a license file. Prefer using GitHub's standard Apache-2.0 license text or create it through the GitHub UI. Do not add a license until the final license decision is made.

Review files before committing:

```bash
git status
```

Stage files:

```bash
git add README.md evidence-purpose.md docs adr launch qa publish .gitignore
```

Commit:

```bash
git commit -m "Add public-safe FinTech external API reference architecture"
```

Create the public GitHub repository:

```bash
gh repo create ktalpay/fintech-external-api-reference-architecture --public --description "Public-safe reference architecture for secure external API access in FinTech payment automation platforms."
```

Check remotes:

```bash
git remote -v
```

If `origin` does not exist, add it:

```bash
git remote add origin https://github.com/ktalpay/fintech-external-api-reference-architecture.git
```

Set main branch:

```bash
git branch -M main
```

Push:

```bash
git push -u origin main
```

Notes:

- If `gh repo create` offers to add a remote automatically, avoid adding a duplicate remote.
- If the repository already exists, skip `gh repo create`.
- If `.gitignore` already exists, review it instead of overwriting it.
- If a license is not final, delay adding `LICENSE`.

## Option B: Manual GitHub UI Flow

1. Open GitHub and create a new repository.
2. Set repository name to `fintech-external-api-reference-architecture`.
3. Set description to `Public-safe reference architecture for secure external API access in FinTech payment automation platforms.`
4. Set visibility to public only after final checklist passes.
5. Do not initialize with README if local files will be pushed.
6. Decide whether to add Apache-2.0 license now or delay licensing.
7. Push local files from the artifact directory.
8. Add topics after push.
9. Verify README render.
10. Verify Mermaid diagram render.
11. Verify docs and ADR links.

## Topics to Add

- `fintech`
- `api-security`
- `external-api`
- `api-key-authentication`
- `multi-tenant`
- `audit-logging`
- `rate-limiting`
- `devsecops`
- `cloud-native`
- `dotnet`
- `architecture`
- `adr`
- `payment-automation`
- `secure-apis`
- `platform-engineering`

## Post-Publication Verification

- Open README.
- Check relative links.
- Check Mermaid rendering.
- Check docs and ADR links.
- Confirm no confidential terms.
- Confirm repository description.
- Confirm topics.
- Confirm license display.
