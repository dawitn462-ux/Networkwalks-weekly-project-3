# Password Cracking with John the Ripper (JTR) & Johnny GUI

A hands-on cybersecurity lab from **Networkwalks Academy** — cracking the passwords on **three** separate password-protected PDFs using **John the Ripper (JTR)** and its GUI front-end, **Johnny**, on Windows.

> ⚠️ **Ethical use only.** This exercise was performed in a controlled training environment against files I was explicitly authorized to test. Password cracking tools must only be used on systems/files you own or have written permission to assess.

---

## 🧠 What I learned

- How **John the Ripper** and **Johnny** work together — JTR does the cracking, Johnny gives it a GUI so you don't need to memorize CLI flags.
- How to pull a crackable **hash** out of a password-protected PDF (the same format used by `pdf2john`/`pdf2hashcat`).
- How a dictionary/brute-force attack recovers a plaintext password from that hash.
- That repeating the attack on three different files with three different passwords drives home the same lesson every time: **the weaker/more common the password, the faster it falls.**

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| [John the Ripper](https://www.openwall.com/john/) | Core password-cracking engine |
| [Johnny](https://openwall.info/wiki/john/johnny) | GUI front-end for JTR |
| Online PDF hash extractor | Converts each locked PDF into a JTR-compatible hash |
| Notepad | Save each extracted hash to a `.txt` file |

---

## ⚙️ One-Time Setup: Installing JTR & Johnny

### Step 1 — Install John the Ripper
Downloaded the Windows build of JTR (jumbo version) from the official site.

### Step 2 — Install & configure Johnny
Downloaded and installed Johnny, the GUI for JTR.

![Download Johnny](01-download-johnny.jpg)
![Installing Johnny](02-install-johnny.jpg)

On first launch, Johnny has no JTR executable configured yet:

![Johnny settings - no JTR path set](03-johnny-settings-empty.jpg)

Pointed Johnny at `john.exe` inside the extracted JTR `run` folder, so it could detect and use the engine:

![Browsing to john.exe](05-browse-john-exe.jpg)
![Johnny detects John the Ripper](04-johnny-settings-john-detected.jpg)

With setup done once, the same workflow below was repeated for all three locked PDFs.

---

## 🔓 Run 1 — My Locked PDF1.pdf

### Extract the hash
Uploaded the protected file to an online PDF-hash-extraction tool, which outputs the hash in the same format JTR's `pdf2john` utility produces.

![Hash extractor tool](06-hash-extractor-site.jpg)
![PDF1 uploaded, hash extracted](07-pdf1-hash-extracted.jpg)

Copied the extracted `$pdf$...` hash value:

![Copy the hash value](08-copy-hash1-value.jpg)

Pasted it into Notepad and saved it as `hash1.txt`:

![Save hash as hash1.txt](09-save-hash1-txt.jpg)

### Load into Johnny and attack
Opened the saved hash file inside Johnny:

![Open password file menu](10-open-password-file-menu.jpg)
![Browse to hash1.txt](11-browse-hash1-file.jpg)

Started the attack:

![Start new attack](12-start-new-attack.jpg)

JTR cracked the hash and recovered the plaintext password:

![PDF1 password cracked](13-pdf1-password-cracked.jpg)

### Unlock the PDF
Entered the recovered password at the prompt and the document opened successfully:

![Password prompt on PDF1](14-pdf1-open-prompt.jpg)
![Entering the cracked password](15-pdf1-enter-password.jpg)

✅ **PDF1 unlocked — flag captured:**

![Flag captured - PDF1](16-pdf1-flag-captured.jpg)

- **Password recovered:** `good-luck`
- **Flag:** `nw{cybersecurity_flag_captured_2608}`

---

## 🔓 Run 2 — My Locked PDF2.pdf

Repeated the same process on the second locked PDF.

Extracted and saved the hash as `hash2.txt`:

![PDF2 hash extracted](17-pdf2-hash-extracted.jpg)
![Save hash as hash2.txt](18-save-hash2-txt.jpg)

Loaded it into Johnny and ran the attack — password recovered:

![PDF2 password cracked](19-pdf2-password-cracked.jpg)

Entered the password to unlock the file:

![Entering PDF2 password](20-pdf2-enter-password.jpg)

✅ **PDF2 unlocked — flag captured:**

![Flag captured - PDF2](21-pdf2-flag-captured.jpg)

- **Password recovered:** `password1`
- **Flag:** `nw{networkwalks_persistence_jtr_270521}`

---

## 🔓 Run 3 — My Locked PDF3.pdf

Same process again on the third locked PDF.

Extracted the hash and saved it as `hash_3.txt`:

![PDF3 hash extracted, saving hash_3.txt](22-pdf3-hash-extracted-save-hash3.jpg)

Browsed to the saved hash file in Johnny:

![Browsing to hash_3 file](23-pdf3-browse-hash3-file.jpg)

JTR cracked the hash, and the recovered password unlocked the file:

![PDF3 password cracked and prompt](24-pdf3-password-cracked-prompt.jpg)

✅ **PDF3 unlocked — flag captured:**

![Flag captured - PDF3](25-pdf3-flag-captured.jpg)

- **Password recovered:** `1qaz2wsx`
- **Flag:** `nw{networkwalks_flag_260821_1}`

---

## 📋 Summary

| File | Hash file | Password Recovered | Flag Captured |
|---|---|---|---|
| My Locked PDF1.pdf | `hash1.txt` | `good-luck` | `nw{cybersecurity_flag_captured_2608}` |
| My Locked PDF2.pdf | `hash2.txt` | `password1` | `nw{networkwalks_persistence_jtr_270521}` |
| My Locked PDF3.pdf | `hash_3.txt` | `1qaz2wsx` | `nw{networkwalks_flag_260821_1}` |

---

## 🔑 Key Takeaway

Running this three times against three different passwords was the real lesson: document-level password protection is only as strong as the password itself. Every single one of these hashes fell within seconds to minutes once loaded into JTR, because the underlying passwords were common/guessable patterns. A hash extracted from a protected PDF can be cracked offline, at speed — strong, unique, high-entropy passwords (or better, passphrase + proper encryption key management) are what actually hold up against this class of attack.

---

## 📚 Reference

Lab: *Week 3 – Project Module 1: Password Cracking with JTR* — Networkwalks Academy
🔗 [www.networkwalks.com](https://www.networkwalks.com)
