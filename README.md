# Networkwalks Cyber Security Internship — Week 3: Password Cracking Lab

## Overview
This repository documents completion of the Week 3 project task/lab from the
**Networkwalks Academy Cyber IT Diploma** internship: extracting password
hashes from locked PDF files and recovering the passwords using dictionary
(wordlist) attacks — the same technique John the Ripper (JtR) uses under the
hood.

Two approaches were used and cross-checked against each other:

1. **Networkwalks' own browser-based tools** — Hash Calculator (PDF → hash
   extraction) and Password Cracker (dictionary attack simulator)
2. **John the Ripper / Johnny (GUI)** running locally, using a hash pulled
   from Online HashCrack's PDF Hash Extractor, to validate the result with
   industry-standard tooling

## Lab Objective
Given password-protected PDF files (`My Locked PDF1.pdf`, `My Locked
PDF2.pdf`, `My Locked PDF3.pdf`), extract a crackable hash (`$pdf$...`
format, pdf2john/pdf2hashcat compatible) and recover the original password
via dictionary attack, then unlock the PDF to retrieve the embedded flag.

## Steps Performed

### 1. Hash extraction
- Downloaded the lab task sheet and locked PDFs from the Networkwalks task
  page.
- Uploaded `My-Locked-PDF1.pdf` to the Networkwalks **Hash Calculator**
  (PDF parsed locally in-browser), which returned a `$pdf$4*4*128*...`
  hash — Revision 4, Version 4, 128-bit key.

### 2. Dictionary attack (Networkwalks Password Cracker)
- Pasted the extracted `$pdf$` hash into the **Password Cracker** tool.
- Ran the built-in 100-word list against it.
- Cracked at attempt 91/100 → password: **`password1`**.
- Used the password to unlock the PDF and captured **Flag 1**:
  `nw{networkwalks_flag1_jtr_270521_1}`

### 3. Second PDF, same method
- Repeated hash extraction and cracking for `My-Locked-PDF2.pdf`.
- Recovered password `password1` again, unlocked the file, and captured
  **Flag 2**: `nw{networkwalks_persistence_jtr_270521}`

### 4. Validation with John the Ripper (Johnny GUI)
- Installed John the Ripper (jumbo build) and pointed the **Johnny** GUI to
  the `john.exe` executable.
- Extracted the hash for `My-Locked-PDF2.pdf` independently using Online
  HashCrack's **PDF Hash Extractor** tool.
- Loaded the hash into Johnny, ran the attack, and confirmed the same
  password (`password1`) was recovered — validating the browser-tool result
  against a real offline cracking tool.

## Key Takeaways
- PDF encryption can be represented as a crackable hash (`$pdf$` format)
  independent of the PDF reader, using `pdf2john`/`pdf2hashcat`-style
  extraction.
- Dictionary attacks succeed quickly against weak/common passwords —
  `password1` was cracked in under 100 attempts.
- Cross-validating a result with a second, independent tool (Johnny/JtR)
  is good practice to confirm findings before reporting them.

## Evidence
screenshots of every step captured and are named
step: hash extraction, the dictionary attack running, the cracked password,
both captured flags, and the Johnny/JtR validation run.

## Disclaimer
This lab was completed on files explicitly provided by Networkwalks Academy
for training purposes as part of an authorized internship exercise. The
techniques and tools shown here (pdf2john, dictionary attacks, John the
Ripper) are standard, publicly available security-auditing tools intended
for testing systems/files you own or are authorized to test.

---
**Program:** Networkwalks Academy — Cyber IT Diploma / Ethical Hacking Internship
**Week:** 3 — Password Cracking with Networkwalks Tools
