# Offensive Security Research — Ezz elden Hisham (APHP)

> **Researcher:** Ezz elden Hisham | **Handle:** APHP | **GitHub:** [@tlvxyou](https://github.com/tlvxyou)
> **Specialization:** White-Box Source Code Review · Black-Box Web & API Exploitation · Supply-Chain Security

---

## 📁 Repository Index

This repository hosts my public-facing security assessments and web exploitation research. All reports reflect original work with accurate, conservative risk contextualization.

---

## 📋 Security Assessments (`assessments/`)

### Leantime v3.4.12 — Independent Source Code & Runtime Hardening Audit

| Field | Details |
|---|---|
| **Target** | Leantime v3.4.12 (PHP/Laravel open-source project management platform) |
| **Scope** | Independent local source-code review and runtime hardening assessment |
| **Methodology** | Static white-box source code audit + black-box dynamic validation (Burp Suite) |
| **Report** | [📄 Leantime-Whitebox-Security-Assessment-Report.pdf](./assessments/Leantime-Whitebox-Security-Assessment-Report.pdf) |

**Audit Scope & Objectives:**

This was an **independent local source-code and runtime hardening audit** conducted to evaluate four specific defense-in-depth control areas:

1. **Cryptographic token derivation** — Reviewing `SHA1(CONCAT(id, sessionPassword))` session token construction vs. CSPRNG-derived alternatives.
2. **File upload MIME/magic-byte normalization** — Evaluating server-side content-type validation and magic-byte enforcement on the avatar/upload endpoint.
3. **Avatar endpoint authorization** — Testing whether object ownership was enforced cryptographically or only by session authentication (IDOR surface).
4. **CSPRNG controls** — Comparing `random_bytes()` usage against `str_shuffle()` patterns in token and key generation paths.

**Architectural & Defense-in-Depth Hardening Findings:**

| CWE | Finding | Accurate Preconditions |
|---|---|---|
| CWE-330 / CWE-338 | Session token derived via `SHA1(CONCAT(id, sessionPassword))` — weaker than a CSPRNG-derived token | Exploitability requires prior leakage of `sessionPassword`; without that, token space remains large. Finding flags the derivation architecture as a hardening gap. |
| CWE-327 | SHA-1 used in security-sensitive token derivation | SHA-1 is collision-weak; the risk here is architectural rather than immediately exploitable under normal conditions. |
| CWE-434 | Server-side MIME/magic-byte validation absent on upload endpoint | Exploitability requires the server's upload directory to be web-accessible and writeable. The finding identifies the missing server-side normalization layer. |
| CWE-639 | Avatar/project object access gated by session auth but not cryptographic ownership binding | An authenticated session can enumerate sequential object IDs. The finding identifies missing ownership-bound access control — horizontal escalation within the authenticated tier. |

**Note on Severity Framing:** These findings are presented as **architectural and defense-in-depth hardening observations** rather than exploits-in-the-wild. Technical hiring managers will note that CWE-330/327 require `sessionPassword` pre-knowledge, and CWE-434 requires a misconfigured server. The audit is intended to demonstrate systematic code review methodology, not to overstate exploitability.

---

## 🔬 Web Exploitation Research (`research/`)

### 1. DNS Rebinding — SOP Bypass Architecture

| Field | Details |
|---|---|
| **Topic** | DNS Rebinding Attacks & Same-Origin Policy Bypass |
| **Technique** | Time-of-check/time-of-use DNS TTL manipulation |
| **Report** | [📄 DNS-Rebinding-SOP-Bypass-Architecture.pdf](./research/DNS-Rebinding-SOP-Bypass-Architecture.pdf) |

**CWE Mapping:** CWE-346 (Origin Validation Error)

**Key Takeaways:**
- DNS rebinding exploits the gap between DNS resolution and HTTP request processing
- Browsers trust same-origin responses even after IP re-binding occurs
- Mitigations: private network access controls, DNS rebinding detection, host header validation

---

### 2. Cookie Sandwich Attack — HttpOnly Bypass Mechanics

| Field | Details |
|---|---|
| **Topic** | Cookie Sandwiching as an HttpOnly Bypass Vector |
| **Technique** | Header injection via malformed Set-Cookie ordering |
| **Report** | [📄 Cookie-Sandwich-HttpOnly-Bypass-Mechanics.pdf](./research/Cookie-Sandwich-HttpOnly-Bypass-Mechanics.pdf) |

**CWE Mapping:** CWE-1004 (Sensitive Cookie Without 'HttpOnly' Flag bypass)

**Key Takeaways:**
- HttpOnly flags can be bypassed when response header ordering is exploitable
- Cookie jar poisoning allows attacker-controlled values to shadow legitimate session tokens
- Mitigations: strict cookie parsing, `__Host-` prefix enforcement, response header auditing

---

### 3. Chaining Blind SSRF to Internal RCE

| Field | Details |
|---|---|
| **Topic** | Blind SSRF Chaining to Internal Service Compromise |
| **Technique** | SSRF → Internal port scan → Service exploitation → RCE |
| **CWE** | CWE-918 (Server-Side Request Forgery) + CWE-78 (OS Command Injection) |
| **Report** | [📄 Chaining-Blind-SSRF-to-Internal-RCE.pdf](./research/Chaining-Blind-SSRF-to-Internal-RCE.pdf) |

**Key Takeaways:**
- Blind SSRF (no visible response body) can still be weaponized via timing side-channels
- Internal services often run without authentication, assuming network perimeter security
- SSRF-to-RCE chains are high-impact and commonly overlooked in web application assessments
- Mitigations: egress filtering, private IP blocklists, metadata endpoint protection

---

## 🏆 Related Public Work

| Repository | Description |
|---|---|
| [GigSphere-Web-Security-Lab](https://github.com/tlvxyou/GigSphere-Web-Security-Lab) | Full-stack vulnerable vs. hardened Flask app (OS Cmd Injection, SSRF, SSTI + 5 more) |
| [java-agent-supply-chain-audit](https://github.com/tlvxyou/java-agent-supply-chain-audit) | JVM bytecode audit + strace/tcpdump dynamic analysis of untrusted Java agent (air-gapped VM) |
| [scriptCTF-2026-wpm-game](https://github.com/tlvxyou/scriptCTF-2026-wpm-game) | PyJail white-box source review & eval() filter bypass (scriptCTF 2026, 444 pts) |
| [subdomain-tool](https://github.com/tlvxyou/subdomain-tool) | Automated subdomain enumeration & recon tooling |

---

## 📬 Contact

- **GitHub:** [github.com/tlvxyou](https://github.com/tlvxyou)
- **Email:** ezzelden.hisham.mohamed@gmail.com
