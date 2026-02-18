---
name: security-audit
description: Run a comprehensive security audit on the current project
---

# Security Audit

When invoked, perform the following steps:

## 1. Identify Project Type and Structure

Examine project configuration files to determine the technology stack:
- `package.json` (Node.js, npm/yarn)
- `requirements.txt` or `pyproject.toml` (Python)
- `go.mod` (Go)
- `pom.xml` or `build.gradle` (Java)
- `Cargo.toml` (Rust)
- Other relevant config files

Document the project type, frameworks, and key directories.

## 2. Use the Security-Audit Skill

Read and apply the security-audit skill to systematically check each OWASP Top 10 category.

## 3. Search for Dangerous Patterns

Use Grep to search for high-risk patterns across the codebase:

- **Code execution**: `eval`, `exec`, `Function()`, `setTimeout`/`setInterval` with string args
- **DOM injection**: `innerHTML`, `document.write`, `dangerouslySetInnerHTML`
- **SQL injection**: String concatenation in queries, raw SQL without parameterization
- **Hardcoded secrets**: API keys, passwords, tokens, connection strings
- **Deserialization**: `pickle.loads`, `ObjectInputStream`, `unserialize`
- **Path traversal**: Unvalidated file paths, user input in `fs.readFile`, `open()`
- **Command injection**: `exec`, `system`, `shell_exec`, `child_process.exec` with user input

## 4. Check Configuration Files

Review configuration files for security misconfigurations:
- Debug mode enabled in production
- Default credentials
- Overly permissive CORS
- Insecure TLS/SSL settings
- Exposed admin endpoints

## 5. Check Security Headers

Search server code for missing or weak security headers:
- Content-Security-Policy
- X-Content-Type-Options
- X-Frame-Options
- Strict-Transport-Security
- X-XSS-Protection (legacy)

## 6. Produce Findings Report

Create a prioritized findings report in table format:

| Priority | Category | Finding | Location | Remediation |
|----------|----------|---------|----------|-------------|
| Critical | ... | ... | ... | ... |
| High | ... | ... | ... | ... |
| Medium | ... | ... | ... | ... |
| Low | ... | ... | ... | ... |

## 7. Executive Summary

End with:
- **Executive Summary**: 2–3 paragraph overview of security posture
- **Top 3 Action Items**: Concrete, prioritized remediation steps
