# Offensive Security Research — Ezz elden Hisham (APHP)

> **Researcher:** Ezz elden Hisham | **Handle:** APHP | **GitHub:** [@tlvxyou](https://github.com/tlvxyou)
> **Specialization:** Hybrid White-Box Source Code Auditing · Black-Box Web & API Exploitation · Supply-Chain Security

---

## 📁 Repository Index

This repository hosts my public-facing white-box security assessments and web exploitation research. All reports are original work and reflect professional-grade offensive security methodology.

---

## 📋 Security Assessments (`assessments/`)

### 🔴 Leantime v3.4.12 — White-Box & Black-Box Security Assessment

| Field | Details |
|---|---|
| **Target** | Leantime v3.4.12 (PHP/Laravel Project Management SaaS) |
| **Methodology** | White-Box Source Code Audit + Black-Box Dynamic Testing |
| **Report** | [📄 Leantime-Whitebox-Security-Assessment-Report.pdf](./assessments/Leantime-Whitebox-Security-Assessment-Report.pdf) |

**Findings Summary:**

| CWE | Vulnerability | Severity |
|---|---|---|
| CWE-330 | Insufficient Randomness in Token Generation | High |
| CWE-327 | Use of a Broken or Risky Cryptographic Algorithm | High |
| CWE-434 | Unrestricted Upload of Dangerous File Types | Critical |
| CWE-639 | Authorization Bypass Through User-Controlled Key (IDOR) | High |
| CWE-338 | Use of Cryptographically Weak PRNG | Medium |

**Key Takeaways:**
- Exposed IDOR vulnerabilities allowing horizontal privilege escalation across project boundaries
- Insecure file upload validation enabling server-side code execution via crafted payloads
- Session token entropy insufficient for cryptographic security guarantees

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
- Mitigations: strict cookie parsing, __Host- prefix enforcement, response header auditing

---

### 3. Chaining Blind SSRF to Internal RCE

| Field | Details |
|---|---|
| **Topic** | Blind SSRF Chaining to Internal Service Compromise |
| **Technique** | SSRF → Internal port scan → Service exploitation → RCE |
| **CWE** | CWE-918 (Server-Side Request Forgery) + CWE-78 (OS Command Injection) |
| **Report** | [📄 Chaining-Blind-SSRF-to-Internal-RCE.pdf](./research/Chaining-Blind-SSRF-to-Internal-RCE.pdf) |

**Key Takeaways:**
- Blind SSRF (no visible response) can still be weaponized via timing side-channels
- Internal services often run without authentication, assuming network perimeter security
- SSRF-to-RCE chains are high-impact and commonly overlooked in web application assessments
- Mitigations: egress filtering, private IP blocklists, metadata endpoint protection

---

## 🏆 Related Public Work

| Repository | Description |
|---|---|
| [GigSphere-Web-Security-Lab](https://github.com/tlvxyou/GigSphere-Web-Security-Lab) | Full-stack vulnerable vs. hardened Flask app (OS Cmd Injection, SSRF, SSTI + 5 more) |
| [java-agent-supply-chain-audit](https://github.com/tlvxyou/java-agent-supply-chain-audit) | JVM bytecode audit + strace/tcpdump dynamic analysis of untrusted Java agent |
| [scriptCTF-2026-wpm-game](https://github.com/tlvxyou/scriptCTF-2026-wpm-game) | PyJail white-box source review & eval() filter bypass (scriptCTF 2026, 441 pts) |
| [subdomain-tool](https://github.com/tlvxyou/subdomain-tool) | Automated subdomain enumeration & recon tooling |

---

## 📬 Contact

- **GitHub:** [github.com/tlvxyou](https://github.com/tlvxyou)
- **Email:** ezzelden.hisham.mohamed@gmail.com
