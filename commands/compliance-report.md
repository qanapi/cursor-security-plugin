---
name: compliance-report
description: Generate a compliance matrix against OWASP Top 10 and SANS/CWE Top 25
---

# Compliance Report

When invoked, perform the following steps:

## 1. Analyze Codebase Structure

Identify all security-relevant code:
- Authentication and authorization logic
- Input handling and validation
- Database access and queries
- File operations
- External API calls
- Serialization/deserialization
- Cryptography usage
- Session management

## 2. OWASP Top 10 (2021) Compliance Matrix

Map findings against each control. Use status: **PASS** / **FAIL** / **NEEDS REVIEW** / **N/A**

| ID | Control | Status | Evidence |
|----|---------|--------|----------|
| A01 | Broken Access Control | | |
| A02 | Cryptographic Failures | | |
| A03 | Injection | | |
| A04 | Insecure Design | | |
| A05 | Security Misconfiguration | | |
| A06 | Vulnerable and Outdated Components | | |
| A07 | Identification and Authentication Failures | | |
| A08 | Software and Data Integrity Failures | | |
| A09 | Security Logging and Monitoring Failures | | |
| A10 | Server-Side Request Forgery (SSRF) | | |

Include code references (file:line or snippet) for each status.

## 3. SANS/CWE Top 25 (2023) Compliance Matrix

Map findings against each weakness. Use status: **PASS** / **FAIL** / **NEEDS REVIEW** / **N/A**

| CWE | Weakness | Status | Evidence |
|-----|----------|--------|----------|
| CWE-787 | Out-of-bounds Write | | |
| CWE-79 | Cross-site Scripting (XSS) | | |
| CWE-89 | SQL Injection | | |
| CWE-416 | Use After Free | | |
| CWE-78 | OS Command Injection | | |
| CWE-20 | Improper Input Validation | | |
| CWE-125 | Out-of-bounds Read | | |
| CWE-22 | Path Traversal | | |
| CWE-352 | CSRF | | |
| CWE-434 | Unrestricted File Upload | | |
| CWE-862 | Missing Authorization | | |
| CWE-476 | NULL Pointer Dereference | | |
| CWE-287 | Improper Authentication | | |
| CWE-190 | Integer Overflow | | |
| CWE-502 | Deserialization of Untrusted Data | | |
| CWE-77 | Command Injection | | |
| CWE-119 | Buffer Overflow | | |
| CWE-798 | Hardcoded Credentials | | |
| CWE-918 | SSRF | | |
| CWE-306 | Missing Authentication | | |
| CWE-362 | Race Condition | | |
| CWE-269 | Improper Privilege Management | | |
| CWE-94 | Code Injection | | |
| CWE-863 | Incorrect Authorization | | |
| CWE-276 | Incorrect Default Permissions | | |

Include code references for each status.

## 4. Overall Compliance Percentage

Calculate:
- OWASP compliance: (PASS + N/A) / 10 × 100%
- CWE compliance: (PASS + N/A) / 25 × 100%
- Combined or weighted overall percentage

## 5. Top 5 Remediation Priorities

List the top 5 remediation priorities based on:
- FAIL or NEEDS REVIEW status
- Severity and exploitability
- Alignment with OWASP and CWE rankings
