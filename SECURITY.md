<div align="center">

# Security Policy

**CONCAP** · Control de Captación

</div>

---

> [!WARNING]
> **Never report a security issue through a public channel.**
> Do not open a GitHub issue, a pull request, a discussion, or a social media post. Use the private process described below.

<br/>

## Why this matters here

CONCAP is not a library or a web service. It is a **deployed cyber-physical system** that controls the water intake of an aqueduct serving a real community.

A vulnerability in this class of system does not leak data — it can interrupt water supply, or worse, allow contaminated water into a distribution network. Responsible disclosure is therefore treated with the seriousness of an operational safety matter, not a software bug.

<br/>

## Scope

### In scope

| Area | Examples |
|:---|:---|
| **Deployed installation** | Weaknesses in the control logic, actuation safety, or fail-safe behavior of the operating system. |
| **Communications** | Issues affecting the ESP-NOW field link, MQTT transport, or session authentication. |
| **Mobile application** | Authentication, authorization, or command-integrity weaknesses in the operator app. |
| **This repository** | Accidental disclosure of credentials, endpoints, keys, calibration data, or any proprietary material that should have been withheld. |

> The last row matters most for external readers. If you find **anything in this repository that appears to expose sensitive information**, that is a valid and valuable report.

### Out of scope

- Vulnerabilities in third-party components reported to their own maintainers (Espressif, Flutter, broker vendors).
- Theoretical attacks requiring physical access to the sealed enclosure at the intake site.
- Findings from automated scanners without a demonstrated impact.
- Requests for source code, schematics, or firmware framed as security research.

<br/>

## How to report

**Preferred channel — GitHub Private Vulnerability Reporting**

Use the **Security → Report a vulnerability** tab of this repository. Reports submitted this way are private and visible only to the maintainer.

**Alternative channel — Email**

Write to **drvillamil94@gmail.com**. Use a clear subject line:

```
[SECURITY] CONCAP — brief description
```

<br/>

### What to include

A good report lets the issue be reproduced and assessed without further exchange:

1. **Component affected** — field node, control node, communications, mobile app, or repository content.
2. **Description** — what the weakness is, in plain technical terms.
3. **Reproduction steps** — the minimum sequence needed to observe it.
4. **Impact assessment** — what an attacker could achieve, with emphasis on any physical or water-safety consequence.
5. **Environment** — versions, conditions, or configuration relevant to the finding.
6. **Suggested mitigation** — optional, but appreciated.
7. **Attribution preference** — whether you wish to be credited publicly.

<br/>

## Response process

| Stage | Target |
|:---|:---|
| **Acknowledgement of receipt** | Within **72 hours** |
| **Initial assessment and severity triage** | Within **7 days** |
| **Status updates during remediation** | Every **14 days** until resolution |
| **Remediation of critical findings** | Prioritized ahead of all other work |

Severity is assessed with **water-safety impact weighted above confidentiality impact**. An issue that could allow contaminated water into the network is treated as critical regardless of how difficult it is to exploit.

<br/>

## Disclosure policy

- Please allow a **90-day** coordinated disclosure window before making a finding public.
- If a finding affects the deployed installation, the aqueduct operators are notified and a mitigation is applied in the field **before** any public discussion.
- Reporters who follow this process will be **credited in [CHANGELOG.md](CHANGELOG.md)** unless they prefer to remain anonymous.
- Good-faith research conducted under this policy will not be met with legal action. This assurance does not extend to unauthorized access to the physical installation or to the aqueduct's infrastructure.

<br/>

## A note on what is not here

This repository intentionally excludes firmware, schematics, credentials, endpoints, and calibration models. That exclusion is itself a security control.

If you are analyzing this project, please note that **absence of detail is deliberate** — requests to disclose withheld material in order to "properly assess security" will be declined.

<br/>

---

<div align="center">
<sub>Thank you for helping keep a community's water supply safe.</sub>
</div>
