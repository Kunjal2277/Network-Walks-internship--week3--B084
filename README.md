# Network-Walks-internship--week3--B084
lab 3 cryptographic hash generation using john the ripper GUI (johnny) and network walks built in tools 
# 🔐 Cryptographic Hash Verification & Password Strength Auditing Lab

> **Internship Project — Week 3**  
> A practical lab documenting cryptographic hash generation via Network Walks built-in utilities and controlled credential strength auditing using **Johnny** (the graphical user interface for **John the Ripper**).

---

## 📌 Overview

Understanding how authentication systems store credentials—and how weak configurations can be identified—is fundamental to defensive security. This repository documents the methodology, workflow, and findings from Week 3 of my cybersecurity internship.

The lab is divided into two core phases:
1. **Hash Generation & Analysis:** Using Network Fox's built-in password and hash calculator to generate cryptographic digests and observe how algorithms transform plain-text strings.
2. **Strength Auditing:** Utilizing **Johnny (John the Ripper GUI)** to perform authorized dictionary and rule-based audits against test hashes to evaluate password resilience.

---

## 🛠️ Tools & Environment

* **Audit Engine:** [John the Ripper](https://www.openwall.com/john/) (Community Enhanced / Jumbo)
* **Graphical Interface:** [Johnny](https://openwall.info/wiki/john/johnny) (Open-source cross-platform GUI for John the Ripper)
* **Hash Utility:** Network Fox Built-in Password & Hash Calculator
* **Wordlists:** `rockyou.txt` / Custom policy-based test lists

---

## 🚀 Lab Workflow

### Phase 1: Hash Generation (Network Walks Calculator)
1. Opened the built-in password and hash calculator utility within the Network Walks environment in which wordlists can be updated.
2. Generated sample test credentials ranging from simple dictionary words to complex passphrases.
3. Computed corresponding cryptographic hashes across standard formats (`MD5`, `SHA-1`, `SHA-256`, and `NTLM`).
4. Exported the generated hash digests into a structured `.txt` file (`sample_hashes.txt`) formatted for auditing.

### Phase 2: Controlled Auditing with Johnny
1. Launched **Johnny** and loaded the `sample_hashes.txt` file via **Open Passwd File**.
2. Configured the hash format auto-detection and verified target algorithm alignment.
3. Executed audits across two modes:
   * **Dictionary Mode:** Tested against standard leaked-password wordlists to benchmark exposure to common patterns.
   * **Rule-Based / Incremental Mode:** Applied mangling rules (capitalization, digit appending, symbol substitution) to evaluate resistance against predictable mutations.
4. Monitored real-time session statistics (guesses per second, time elapsed, and recovery ratio) through the Johnny dashboard.

---

## 📊 Key Observations & Findings

| Password Pattern | Example Format | Hashing Algorithm | Audit Outcome | Mitigation |
| :--- | :--- | :--- | :--- | :--- |
| Common dictionary word | `password123` | MD5 | Resolved immediately | Enforce blocklists for known breached passwords |
| Simple mutation | `Summer2026!` | SHA-256 (Unsalted) | Resolved via mangling rules | Implement unique per-user cryptographic salts |
| Random passphrase | `4-word-uncorrelated-phrase` | Salted SHA-512 / bcrypt | Unresolved within audit window | Mandate length ($\ge 14$ chars) and slow KDFs (`Argon2id`, `bcrypt`) |

---

## 🛡️ Security Recommendations

* **Deprecate Fast/Legacy Hashes:** Avoid using `MD5`, `SHA-1`, or unsalted `SHA-256` for credential storage due to high-speed GPU calculation risks.
* **Adopt Slow Key Derivation Functions:** Use memory-hard algorithms like **Argon2id**, **bcrypt**, or **PBKDF2** with high iteration counts.
* **Implement Unique Salts:** Ensure every credential entry uses a cryptographically random salt to neutralize precomputed lookup tables.

---

## ⚠️ Legal & Ethical Disclaimer

*This project was conducted strictly within an isolated lab environment using self-generated test hashes for educational and defensive auditing purposes during a supervised internship. Do not run auditing tools against systems or credential files without explicit written authorization.*
