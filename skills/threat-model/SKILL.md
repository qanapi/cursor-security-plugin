---
name: threat-model
description: Guide STRIDE-based threat modeling for a feature, component, or system architecture. Use when designing new features, reviewing architecture, or assessing risk for existing systems.
---

# Threat Model (STRIDE)

## Overview

Guides STRIDE-based threat modeling to identify security threats for a feature, component, or system. Identifies assets, trust boundaries, data flows, and entry points, then applies STRIDE systematically to assess and mitigate risks.

## When to Use

- Designing new features or components
- Reviewing system or service architecture
- Assessing risk for existing systems
- User requests threat modeling, risk assessment, or security design review

## Instructions

### 1. Gather Context

- **Ask the user** to describe the feature, component, or system (or read the code/architecture)
- Identify: purpose, technologies, integrations, and any existing security controls

### 2. Identify Key Elements

Document:

- **Assets**: What needs protection? (user data, credentials, API keys, PII, intellectual property)
- **Trust boundaries**: Where does trust change? (user ↔ app, app ↔ backend, microservice boundaries, third-party APIs)
- **Data flows**: How does data move? (user input → API → DB, webhook → handler → queue)
- **Entry points**: Where can external actors interact? (HTTP endpoints, webhooks, file uploads, CLI, SDK)

### 3. Apply STRIDE Systematically

For each element (component, data flow, entry point), evaluate:

| Category | Question | Examples |
|----------|----------|----------|
| **Spoofing** | Can an attacker impersonate a user or component? | Forged JWT, stolen session, fake webhook caller |
| **Tampering** | Can data be modified in transit or at rest? | Man-in-the-middle, DB compromise, request tampering |
| **Repudiation** | Can actions be denied without evidence? | No audit logs, missing request IDs |
| **Information Disclosure** | Can sensitive data leak? | Logs, error messages, enumeration, over-permissive APIs |
| **Denial of Service** | Can availability be disrupted? | Resource exhaustion, rate limit bypass, expensive operations |
| **Elevation of Privilege** | Can an attacker gain unauthorized access? | Missing authorization, privilege escalation, IDOR |

### 4. Assess Each Threat

For each identified threat:

- **Likelihood**: Low / Medium / High (ease of exploitation, attacker motivation)
- **Impact**: Low / Medium / High (data loss, downtime, compliance, reputation)
- **Risk Level**: Derive from likelihood × impact (e.g., High+High = Critical)

### 5. Suggest Mitigations

For each threat, propose mitigations with priority (must-have vs nice-to-have).

### 6. Produce Threat Matrix Table

Output a markdown table:

| Threat Category | Threat Description | Likelihood | Impact | Risk Level | Mitigation |
|-----------------|-------------------|------------|--------|------------|------------|
| ... | ... | ... | ... | ... | ... |

### 7. Data Flow Diagram

Produce a data flow diagram description in Mermaid syntax (flowchart or sequence diagram) showing:

- External actors
- Components/systems
- Trust boundaries (dashed lines or swimlanes)
- Data flows and direction

## Output Format

```markdown
# Threat Model: [Feature/Component/System Name]

## Context

[Brief description of scope and technologies]

## Assets

- [Asset 1]
- [Asset 2]

## Trust Boundaries

- [Boundary 1]
- [Boundary 2]

## Entry Points

- [Entry point 1]
- [Entry point 2]

## Threat Matrix

| Threat Category | Threat Description | Likelihood | Impact | Risk Level | Mitigation |
|-----------------|-------------------|------------|--------|------------|------------|
| ... | ... | ... | ... | ... | ... |

## Data Flow Diagram

\`\`\`mermaid
flowchart LR
    User -->|HTTPS| API
    API -->|Trust Boundary| DB
\`\`\`

## Summary

[Top risks and recommended priorities]
```

## References

- [STRIDE (Microsoft)](https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-threats)
- [OWASP Threat Modeling](https://owasp.org/www-community/Threat_Modeling)
- [Mermaid Flowchart Syntax](https://mermaid.js.org/syntax/flowchart.html)
