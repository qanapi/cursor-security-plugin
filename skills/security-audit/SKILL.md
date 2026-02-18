---
name: security-audit
description: Perform a structured security audit of code, systematically checking each OWASP Top 10 category and SANS/CWE Top 25 weakness. Use when reviewing files, modules, PRs, or entire projects for security vulnerabilities.
---

# Security Audit

## Overview

Performs a systematic security audit of a target codebase (file, directory, or PR diff), walking through OWASP Top 10 (2021) and SANS/CWE Top 25 categories, flagging vulnerabilities with severity ratings and remediation guidance.

## When to Use

- Reviewing files, modules, PRs, or entire projects for security vulnerabilities
- Pre-merge security checks
- Compliance or audit preparation
- User explicitly requests a security audit or vulnerability assessment

## Instructions

### 1. Accept the Target

Identify the audit scope from the user:
- **File**: Single source file
- **Directory**: Path to a module or subdirectory
- **PR diff**: Staged or unstaged changes, or a diff from a pull request

If no target is specified, ask the user or default to the current working directory.

### 2. Walk Through OWASP Top 10 (2021) Systematically

For each category below, search for relevant patterns using the Grep tool and flag findings.

| Category | Key Patterns to Search |
|----------|------------------------|
| **A01 Broken Access Control** | `isAdmin`, `role`, `permission`, `authorize`, path traversal (`../`), IDOR patterns, missing auth checks |
| **A02 Cryptographic Failures** | `md5`, `sha1`, `DES`, `RC4`, `eval`, weak crypto, plaintext passwords, unencrypted storage |
| **A03 Injection** | `eval`, `exec`, `innerHTML`, SQL string concatenation, `+` with user input in queries, `document.write`, `dangerouslySetInnerHTML` |
| **A04 Insecure Design** | Missing rate limits, lack of input validation, insecure defaults |
| **A05 Security Misconfiguration** | Debug mode in prod, default credentials, verbose errors, CORS `*`, insecure headers |
| **A06 Vulnerable Components** | Outdated dependencies, known CVEs in package.json/requirements.txt/go.mod |
| **A07 Auth Failures** | Hardcoded passwords, weak session handling, missing MFA, credential stuffing vectors |
| **A08 Integrity Failures** | Unsigned downloads, missing integrity checks, insecure deserialization |
| **A09 Logging Failures** | Missing audit logs, logging sensitive data (passwords, tokens), log injection |
| **A10 SSRF** | `fetch`, `request`, `http.get`, user-controlled URLs, internal IP/domain access |

### 3. Use Grep for Known Dangerous Patterns

Run targeted Grep searches for:

- `eval(`, `exec(`, `Function(`
- `innerHTML\s*=`, `dangerouslySetInnerHTML`
- SQL: `"SELECT.*\+`, `'SELECT.*\+`, string concatenation in queries
- `password\s*=\s*["']`, `secret\s*=\s*["']`, `api_key\s*=\s*["']`
- `BEGIN RSA PRIVATE KEY`, `BEGIN EC PRIVATE KEY`, `BEGIN OPENSSH PRIVATE KEY`
- `localhost`, `127.0.0.1` in fetch/request URLs with user input
- `document\.write(`, `document\.cookie`
- `process\.env` used unsafely or fallback to hardcoded values

### 4. Rate Each Finding

Assign severity using this scale:

| Severity | Criteria |
|----------|----------|
| **Critical** | Direct RCE, SQL injection, auth bypass, credential exposure |
| **High** | XSS, SSRF, insecure deserialization, missing auth on sensitive endpoints |
| **Medium** | Weak crypto, IDOR, information disclosure, misconfiguration |
| **Low** | Best-practice violations, verbose errors, missing headers |
| **Info** | Recommendations, defense-in-depth improvements |

### 5. Produce the Findings Table

Output a markdown table with columns:

| Severity | Finding | Location | OWASP/CWE | Remediation |
|----------|---------|----------|-----------|-------------|
| ... | ... | file:line | A0X / CWE-XXX | Specific fix |

### 6. Executive Summary

End the audit with:

1. **Total findings by severity**: Count of Critical, High, Medium, Low, Info
2. **Overall risk rating**: Critical / High / Medium / Low based on highest-severity findings
3. **Top 3 priorities**: Ordered list of the most urgent remediations

## Output Format

```markdown
# Security Audit Report

**Target:** [path or scope]
**Date:** [date]

## Findings

| Severity | Finding | Location | OWASP/CWE | Remediation |
|----------|---------|----------|-----------|-------------|
| ... | ... | ... | ... | ... |

## Executive Summary

- **Total findings:** X Critical, X High, X Medium, X Low, X Info
- **Overall risk rating:** [Critical/High/Medium/Low]
- **Top 3 priorities:**
  1. [Priority 1]
  2. [Priority 2]
  3. [Priority 3]
```

## References

- [OWASP Top 10 (2021)](https://owasp.org/Top10/)
- [CWE Top 25](https://cwe.mitre.org/top25/)
- [SANS Top 25](https://www.sans.org/top25-software-errors/)
