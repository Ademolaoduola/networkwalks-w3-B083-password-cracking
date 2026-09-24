# networkwalks-w3-B083-password-cracking
Week 3 lab — cracking a password-protected PDF using John the Ripper/Johnny and Networkwalks online tools
# Week 3 Project Report — Password Cracking with JTR and Networkwalks Tools

W3-PM1 | W3-PM2 | CYBERSECURITY | NETWORKWALKS

| Field | Details |
|---|---|
| Pentester Name | Ademola Oduola (Cybersecurity Professional) |
| Program / Batch | B083 - Networkwalks |
| Date | 09/24/2026 |
| Modules completed | W3-PM1 (Password Cracking with JTR)<br>W3-PM2 (Password Cracking with Networkwalks Tools) |
| Target File | My Locked PDF1.pdf |
| Permission secured from client? | Yes — file provided for lab exercise |
| Phases covered | Phase 1: Hash Extraction<br>Phase 2: Password Cracking (Local Tool)<br>Phase 3: Password Cracking (Online Tool) |

## 1. Liability Disclaimer

I have performed these activities only on the file provided for this lab exercise, for education and research purposes only. Do not use anything from here to break the law. The instructor, the authors, and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility.

## 2. Methodology

This exercise was carried out on a **Windows 10 PC**, using two separate approaches to recover the password of an encrypted PDF file:

1. **John the Ripper (JTR) + Johnny GUI** — a locally installed password-cracking suite
2. **Networkwalks Hash Calculator + Password Cracker** — free browser-based tools requiring no installation

Every step below includes:
- The exact tool or command used
- The result observed
- A screenshot as evidence
- A short note on why the finding matters from a security perspective

## 3. Tools Used

| Tool | Purpose |
|---|---|
| John the Ripper (JTR) | Command-line password-cracking tool; recovers passwords from file hashes |
| Johnny | GUI front-end for John the Ripper, for point-and-click password attacks |
| Networkwalks Hash Calculator | Browser-based tool to extract the password hash from a locked PDF |
| Networkwalks Password Cracker | Browser-based tool to crack a password from an extracted hash |
| Windows 10 | Host OS used to run both the local and browser-based tools |

## 4. Background

Password cracking is the process of recovering a password from stored data or a protected file. Security professionals use it to test password strength and demonstrate why weak passwords are a risk — a short or common password can be recovered quickly, while a strong one resists cracking for far longer.

Files such as PDF, ZIP, and Office documents store their password as a **hash** rather than in plain text. A hash is a scrambled, one-way representation of the password. To recover the original password, the hash must first be extracted from the file, then run through a cracking tool that tests candidate passwords (from a wordlist or brute-force pattern) until it finds a match.

---

## 5. Module 1 — Password Cracking with JTR (John the Ripper + Johnny)

### 5.1 Task

Crack the password of the supplied PDF file (`My Locked PDF1.pdf`) using **John the Ripper** and the **Johnny** GUI on a Windows PC.

> Note: On Kali Linux, John the Ripper comes pre-installed and can be opened directly — no download required.

### 5.2 Installation

| Step | Action | Result |
|---|---|---|
| 1 | Downloaded John the Ripper from the official site (openwall.com/john) | JTR binaries obtained for Windows |
| 2 | Downloaded Johnny GUI from openwall.info/wiki/john/johnny | Installer obtained |
| 3 | Ran the Johnny setup file | Johnny installed successfully |
| 4 | Opened Johnny → Settings → Browse | Pointed Johnny to `john.exe` |
| 5 | Located `john.exe` in the `run` folder of the JTR download | Johnny linked to the John the Ripper engine |

### 5.3 Hash Extraction

| Step | Action | Result |
|---|---|---|
| 1 | Downloaded the encrypted file `My Locked PDF1.pdf` | File saved locally |
| 2 | Uploaded the PDF to an online hash extractor (onlinehashcrack.com PDF hash tool) | Hash value generated, prefixed `$pdf$...` |
| 3 | Copied the hash value | Verified no stray characters (e.g. leading `b'`) were included |
| 4 | Pasted the hash into Notepad and saved as `hash1.txt` | Hash file ready for JTR |

> **Note:** The hash must be saved in the exact format the extractor outputs — starting with `$pdf$`. Any extra characters (such as a leading `b'` from a Python byte-string artifact) will cause John the Ripper to fail to parse the hash.

### 5.4 Cracking the Password

| Step | Action | Result |
|---|---|---|
| 1 | Opened Johnny | GUI launched |
| 2 | Clicked "Open password file" and selected `hash1.txt` | Hash loaded into Johnny |
| 3 | Clicked "Start new attack" | John the Ripper began testing candidate passwords |
| 4 | Waited for the attack to complete | Password successfully cracked |
| 5 | Opened `My Locked PDF1.pdf` and entered the recovered password | PDF unlocked successfully |

### 5.5 Observation

John the Ripper recovered the PDF password in [insert time taken] using [insert attack mode — e.g. default wordlist / incremental mode]. This demonstrates that a weak or dictionary-based password can be recovered quickly by an attacker with access to the file's hash, reinforcing the need for long, non-dictionary passwords on sensitive documents.

---

## 6. Module 2 — Password Cracking with Networkwalks Tools

### 6.1 Task

Crack the password of the same PDF file (`My Locked PDF1.pdf`) using the **Networkwalks Hash Calculator** and **Networkwalks Password Cracker** — both free, browser-based tools requiring no installation.

> Note: This method also works on Kali Linux, since both tools run entirely in a web browser.

### 6.2 Steps

| Step | Action | Tool / URL |
|---|---|---|
| 1 | Downloaded the encrypted PDF from the lab page | networkwalks.com (lab download page) |
| 2 | Opened the Networkwalks Hash Calculator | networkwalks.com/hash-calculator |
| 3 | Uploaded the locked PDF file | Tool extracted the hash, prefixed `$pdf$...` |
| 4 | Copied the complete hash value | Confirmed the full string was copied, starting from `$pdf$` |
| 5 | Opened the Networkwalks Password Cracker | networkwalks.com/password-cracker |
| 6 | Pasted the hash and started the attack | Tool began testing candidate passwords |
| 7 | Waited for the attack to complete | Cracked password displayed on screen |
| 8 | Opened the PDF and entered the cracked password | PDF opened successfully |

### 6.3 Observation

The Networkwalks online tools produced the same cracked password as the local John the Ripper method, without requiring any software installation. This shows that password cracking is accessible even without specialist local tooling — browser-based cracking services lower the barrier further, meaning weak document passwords can be broken by almost anyone with an internet connection.

---

## 7. Comparison of Methods

| Aspect | JTR + Johnny (Local) | Networkwalks (Online) |
|---|---|---|
| Installation required | Yes | No |
| Runs offline | Yes | No — requires internet access |
| Platform | Windows / Linux / Mac | Any device with a browser |
| Ease of use for beginners | Moderate (GUI simplifies this) | High (fully guided, no setup) |
| Data privacy | Hash stays local | Hash uploaded to third-party service |

## 8. Key Takeaways

- Both a locally installed tool and a free online tool were able to recover the same password from the same hash, showing that **password strength — not tool availability — is the real defense**.
- Uploading a hash to an online cracking service (as in Module 2) means the hash leaves your machine; for real engagements, this is **not appropriate for sensitive or client data** and local tools like JTR should be used instead.
- This exercise reinforces why organizations should use long, random passphrases (and, where possible, file-level encryption combined with strong access controls) rather than relying on password protection alone.

---
Pentesting Project Report | Networkwalks | Ademola Oduola
