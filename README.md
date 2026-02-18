# Qanapi Security

Security review and compliance enforcement plugin for [Cursor](https://cursor.com). Covers **OWASP Top 10 (2021)**, **SANS/CWE Top 25 (2023)**, and secure coding best practices -- language-agnostic, always-on.

## What's included

| Component | Count | Description |
|-----------|-------|-------------|
| **Rules** | 18 | Always-on secure coding rules that guide every AI response |
| **Skills** | 3 | On-demand deep-dive security capabilities |
| **Agents** | 2 | Specialized security personas |
| **Commands** | 3 | One-shot security actions |

## Installation

Install from the Cursor marketplace, or add directly from the repository:

```
cursor plugin install qanapi-security
```

## Rules

Rules are active on every file the AI touches. Each rule maps to specific OWASP and CWE identifiers.

| Rule | Vulnerability Class | Standards |
|------|-------------------|-----------|
| `injection-prevention` | SQL, NoSQL, OS command, LDAP, code injection | OWASP A03, CWE-89, CWE-78, CWE-77 |
| `xss-prevention` | Reflected, stored, DOM-based XSS | CWE-79 |
| `csrf-protection` | Cross-site request forgery | CWE-352 |
| `authentication-security` | Password storage, session mgmt, brute-force | OWASP A07, CWE-287, CWE-306 |
| `access-control` | Broken access control, IDOR, privilege escalation | OWASP A01, CWE-862, CWE-863 |
| `cryptographic-practices` | Weak algorithms, poor key management | OWASP A02, CWE-327, CWE-328 |
| `input-validation` | Improper input validation | CWE-20 |
| `output-encoding` | Context-dependent output encoding | CWE-116 |
| `secrets-management` | Hardcoded credentials, secrets in source | CWE-798, CWE-259 |
| `error-handling` | Information disclosure through errors | CWE-209, CWE-200 |
| `security-misconfiguration` | Insecure defaults, debug mode, missing headers | OWASP A05, CWE-16 |
| `ssrf-prevention` | Server-side request forgery | OWASP A10, CWE-918 |
| `file-upload-security` | Unrestricted file upload | CWE-434 |
| `path-traversal-prevention` | Directory traversal, file inclusion | CWE-22 |
| `deserialization-safety` | Insecure deserialization | OWASP A08, CWE-502 |
| `dependency-security` | Vulnerable/outdated components | OWASP A06 |
| `logging-monitoring` | Insufficient logging and monitoring | OWASP A09, CWE-778 |
| `secure-defaults` | Secure-by-default patterns | General best practice |

## Skills

Skills are invoked on-demand for deeper analysis.

### security-audit

Performs a structured security review walking through each OWASP Top 10 category. Flags findings with severity (Critical/High/Medium/Low/Info), produces a findings table, and ends with an executive summary.

### threat-model

Guides STRIDE-based threat modeling for a feature or architecture. Identifies Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege risks. Outputs a threat matrix with mitigations and a data flow diagram.

### secrets-scan

Scans code for hardcoded credentials, API keys, tokens, connection strings, and private keys. Checks `.gitignore` coverage and warns that any committed secret should be rotated immediately.

## Agents

### security-reviewer

A senior application security engineer persona. Reviews all code through a security lens, flags vulnerabilities with severity ratings, provides concrete fix suggestions, and references OWASP/CWE IDs in findings.

### compliance-auditor

A compliance-focused auditor that maps code against OWASP Top 10 and SANS/CWE Top 25. Produces structured compliance matrices with PASS/FAIL/NEEDS REVIEW status per control, cites evidence, and recommends remediation priorities.

## Commands

| Command | Description |
|---------|-------------|
| `security-audit` | Run a full security audit on the current project |
| `check-secrets` | Scan the codebase for hardcoded secrets and credentials |
| `compliance-report` | Generate a compliance matrix against OWASP Top 10 and SANS/CWE Top 25 |

## Standards coverage

### OWASP Top 10 (2021)

- **A01** Broken Access Control
- **A02** Cryptographic Failures
- **A03** Injection
- **A04** Insecure Design
- **A05** Security Misconfiguration
- **A06** Vulnerable and Outdated Components
- **A07** Identification and Authentication Failures
- **A08** Software and Data Integrity Failures
- **A09** Security Logging and Monitoring Failures
- **A10** Server-Side Request Forgery (SSRF)

### SANS/CWE Top 25 (2023)

CWE-787, CWE-79, CWE-89, CWE-416, CWE-78, CWE-20, CWE-125, CWE-22, CWE-352, CWE-434, CWE-862, CWE-476, CWE-287, CWE-190, CWE-502, CWE-77, CWE-119, CWE-798, CWE-918, CWE-306, CWE-362, CWE-269, CWE-94, CWE-863, CWE-276

## License

MIT
