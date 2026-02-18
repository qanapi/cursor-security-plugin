---
name: check-secrets
description: Scan the codebase for hardcoded secrets and credentials
---

# Check Secrets

When invoked, perform the following steps:

## 1. Use the Secrets-Scan Skill

Read and apply the secrets-scan skill to search for hardcoded credentials.

## 2. Scan for Secret Types

Scan all source files for:
- **API keys**: AWS, Stripe, OpenAI, GitHub, etc.
- **Passwords**: Plaintext passwords, connection strings with credentials
- **Tokens**: JWT, OAuth tokens, session secrets
- **Connection strings**: Database URLs, Redis, message queues
- **Private keys**: PEM files, SSH keys, certificate material

## 3. Check .gitignore

Verify that `.gitignore` properly excludes secret-bearing files:
- `.env`, `.env.local`, `.env.*`
- `*.pem`, `*.key`, `*.p12`, `*.pfx`
- `secrets.json`, `credentials.json`
- `config.local.*`, `*.secret`

Report any missing exclusions.

## 4. Git History Warning

If secrets are found in tracked files, include this warning:

> **Git History Awareness**: Secrets committed to git remain in history even after removal. To fully remediate, use `git filter-branch` or [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) to purge history. Consider the secret compromised and rotate it immediately.

## 5. Report Format

For each finding, report:
- **File path**
- **Line number**
- **Secret type** (API key, password, token, etc.)
- **Remediation** (move to env var, use secrets manager, rotate, etc.)

## 6. Summary

Provide:
- **Total count by type**: Table of secret types and counts
- **Overall risk assessment**: Critical / High / Medium / Low
- **Emphasis**: Any secret found in source should be rotated immediately—assume it has been exposed.
