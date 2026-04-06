# SurakshaSetu 🛡️
### Federated App Intelligence Network Against Mobile Financial Fraud

[![RBI Framework](https://img.shields.io/badge/Regulatory-RBI%20Framework-blue)](https://www.rbi.org.in/)
[![TRAI DLT](https://img.shields.io/badge/Compliant-TRAI%20DLT-green)](https://www.trai.gov.in/)
[![DPDP 2023](https://img.shields.io/badge/Privacy-DPDP%202023-orange)](https://www.meity.gov.in/)
[![CERT-In](https://img.shields.io/badge/Security-CERT--In-red)](https://www.cert-in.org.in/)

> **Protecting Every Banking Transaction** — A three-layer federated interception network that stops mobile financial fraud at the telecom gateway, on the device, and inside the Core Banking System.

---

## 🚨 Problem

Fraudsters distribute clone banking applications via bulk SMS and WhatsApp, targeting India's **750 million smartphone users**. Sideloaded APKs:

- Harvest credentials through overlay attacks
- Intercept OTPs via Remote Access Trojans
- Grant attackers full device control

**Current defences (CERT-In blacklisting, TRAI sender filters, Play Protect) are reactive**, with a **48–72 hour response lag**. A single campaign reaches lakhs of victims before any block is enforced. No existing mechanism intercepts a phishing link before it reaches the victim's device, nor correlates fraud signals across institutions in real time.

---

## 💡 Core Idea

SurakshaSetu is a **three-layer federated interception network** where each layer independently stops the attack — and all three operate in concert so that evasion of one layer does not result in financial loss.

Protection is enforced simultaneously at:
1. **The telecom gateway** — before delivery
2. **On the device** — before installation
3. **Inside the Core Banking System** — before funds move

---

## 🏗️ Architecture

```
LAYER 1 — NETWORK EDGE       LAYER 2 — DEVICE AGENT       LAYER 3 — BANK CORE
─────────────────────        ──────────────────────        ───────────────────
SMSC / DLT Gateway    ──►    APK Install (Sideload)  ──►   Txn Attempt
URL Scorer                   Agent SDK (YONO)               CBS Engine
Rule-based engine            Hash + Perm-Graph               Risk signal check
BLOCK / PASS                 ALERT + Sync                    OOB IVRS
                                                             Voice verify

            ◄──── FEDERATED THREAT REGISTRY ────►
             Quorum-validated | 15-min consensus
             Hash-only | DPDP-compliant
```

---

## 🔒 Three Layers Explained

### Layer 1 — Network Edge
- Hooks into the **SMSC/DLT gateway**
- Every URL in an inbound SMS or WhatsApp Business message is scored against a live **Threat Registry** before delivery
- High-risk links replaced with a warning redirect in **under 800 ms**
- Integration: TRAI DLT API + telecom SMSC hooks (Jio, Airtel, BSNL, Vi)

### Layer 2 — Device Agent SDK
- Lightweight SDK embedded within **SBI YONO** (under 6 MB, Android Go compatible)
- Monitors APK installation events
- Fingerprints each package's **permission-request graph**
- Detects zero-day variants **without signature updates**
- On alert: full-screen warning served; hash pushed to registry within **90 seconds**

### Layer 3 — Core Banking
- Device-risk signals ingested directly into the **CBS transaction engine**
- Flagged devices trigger **out-of-band IVRS voice verification** — bypassing SMS OTP, which a compromised device can intercept
- Integration: SBI CBS API + NPCI UPI transaction hooks

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 🔍 Pre-installation App Check | APK SHA-256 hash and permission-graph fingerprint validated before installation completes |
| 🔗 URL Scanning Before Click | Telecom-level interception in under 800 ms — covers SMS and WhatsApp Business API |
| 📱 Device-Level Warning | Full-screen alert with block/proceed options; responses logged for cross-institution intelligence |
| 🏛️ Federated Threat Registry | Quorum-validated, hash-only ledger; three-member consensus within 15 minutes; DPDP compliant |
| 📞 OOB IVRS Authentication | Voice verification for flagged devices — eliminates SMS OTP interception |
| 💬 WhatsApp Business Integration | Direct pipeline from India's primary fraud channel into the registry |

---

## 🗺️ User Journey

```
01 Link Received      → Victim receives malicious SMS/WhatsApp URL
02 SMSC Interception  → URL scored against live Threat Registry [NETWORK]
03 Block / Warn       → High-risk links replaced with warning redirect ✅ BLOCKED
04 APK Sideload       → If user proceeds, Device Agent SDK detects sideload
05 Fingerprint Check  → APK hash + permission-graph matched against registry [DEVICE]
06 On-Device Alert    → Full-screen warning; hash pushed to registry ✅ BLOCKED
07 Txn Attempt        → CBS intercepts flagged device transaction
08 OOB Verification   → IVRS voice call triggered — bypasses SMS OTP [CBS]
09 Clearance / Block  → Verified proceeds; unverified held + fraud team alerted ✅ CLEARED
```

---

## 🎯 Unique Selling Proposition

> **No existing Indian solution combines telecom-level interception + on-device fingerprinting + CBS-integrated OOB authentication in a single coordinated framework.**

- **Three-barrier defence**: An attacker must independently defeat all three layers. Evasion of L1 does not bypass L2; evasion of L2 does not bypass L3.
- **Zero-day detection**: Permission-graph fingerprinting catches new APK variants without signature database updates — closing the 48–72 hour window.
- **Privacy-first intelligence sharing**: No raw PII leaves any institution; only cryptographic hashes shared across the Federated Threat Registry (DPDP Act compliant).

---

## 📊 Target Impact

| Metric | Target |
|---|---|
| Threat-to-block time | **< 8 minutes** (down from 48–72 hours) |
| SMS/WhatsApp links intercepted | **85%** blocked at telecom gateway |
| Post-install fraud rate | **< 5%** |
| False positive rate | **< 0.2%** |

---

## ⚙️ Scalability & Feasibility

- **Low-end device support**: Agent SDK runs on Android Go (2 GB RAM), under 6 MB — the exact handset tier exploited by attackers
- **Telecom scale**: URL scoring API integrates via TRAI DLT hooks available to all licensed operators (Jio, Airtel, BSNL, Vi) without custom hardware
- **Minimal user friction**: Warning redirect and on-device alert require a single tap — no additional app installation beyond existing YONO update cycle

---

## 🚀 Phased Rollout

```
Phase 1 (0–6 months)   → YONO SDK + Registry pilot within RBI Regulatory Sandbox
Phase 2 (6–12 months)  → SMSC integration with two operators + PSB onboarding
```

No new legislation required. Deployable under existing:
- RBI Cybersecurity Framework
- TRAI DLT Mandate
- CERT-In CII Obligations

---

## 🏦 Domain & Regulatory Context

| Area | Details |
|---|---|
| Domain | Cybersecurity / Digital Banking |
| Regulatory | RBI \| TRAI \| CERT-In \| DPDP 2023 |
| Deployment | Production-ready in 6–12 months |
| Sandbox | Phase 1 within RBI Regulatory Sandbox |

---

## 📄 License

This project is submitted as part of the **SBI Hackathon**. All rights reserved.

---

*SurakshaSetu — Protecting Every Banking Transaction*
