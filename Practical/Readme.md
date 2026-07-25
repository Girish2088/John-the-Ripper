# John the Ripper Practical Labs

This folder contains the practicals I performed while learning **John the Ripper**.

The goal here isn't just to memorize commands, but to understand the complete workflow of recovering passwords from different types of targets.

Most labs follow the same idea:

```text
Target
   │
   ▼
Identify Target
   │
   ▼
Convert (if required)
   │
   ▼
Run John
   │
   ▼
Recover Password
   │
   ▼
Verify Result
```

---

## What You'll Find Here

Each practical contains:

- Objective
- Commands Used
- Steps Performed
- Expected Output
- Explanation
- Screenshots
- Notes (Things I learned / Mistakes I made)

---

## Practical Labs

### 01. Basic Hash Cracking

Crack a simple password hash using John.

---

### 02. Identify Unknown Hash

Identify an unknown hash using `hash-id.py` before cracking it.

---

### 03. Format-Specific Cracking

Specify the correct hash format manually when automatic detection fails.

---

### 04. Wordlist Attack

Recover passwords using the `rockyou.txt` wordlist.

---

### 05. Single Crack Mode

Use usernames and account information to generate password guesses.

---

### 06. Custom Rules

Create password variations using John's custom rules.

---

### 07. Linux Password Cracking

Combine `/etc/passwd` and `/etc/shadow` using `unshadow`, then recover Linux user passwords.

---

### 08. Windows NTLM Cracking

Crack Windows NTLM password hashes.

---

### 09. ZIP Password Cracking

Convert a password-protected ZIP file using `zip2john`, then recover its password.

---

### 10. RAR Password Cracking

Convert a password-protected RAR archive using `rar2john`, then recover its password.

---

### 11. SSH Key Passphrase Cracking

Extract a hash from an encrypted SSH private key using `ssh2john.py`, then recover its passphrase.

---

### 12. Show Cracked Passwords

Display previously recovered passwords without running the cracking process again.

---

### 13. Troubleshooting

Common issues I faced while practicing, such as:

- Wrong hash format
- Wrong working directory
- Missing converter tools
- Incorrect file paths
- Conversion failures
- "No password hashes loaded" errors

---

## Why I Made These Practicals

While learning John the Ripper, I realized that the hardest part usually isn't remembering the command.

It's understanding:

- What kind of file am I dealing with?
- Does it need conversion first?
- Which format should I use?
- What should I do if John can't detect the hash?

These labs document the complete workflows I practiced, along with screenshots and notes, so I can revisit them later and show practical experience instead of just command memorization.
