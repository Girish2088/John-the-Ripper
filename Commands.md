# John the Ripper Commands

This file contains the John the Ripper commands I learned while practicing.

---

# Basic Syntax

```bash
john [options] <target>
```

Example:

```bash
john hashes.txt
```

---

# Basic Hash Cracking

Let John automatically detect the hash format.

```bash
john hashes.txt
```

---

# Dictionary (Wordlist) Attack

Use a wordlist to recover passwords.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

Example:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

---

# Format-Specific Cracking

If automatic detection fails, specify the hash format manually.

```bash
john --format=<format> --wordlist=<wordlist> hashes.txt
```

Example:

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Example:

```bash
john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Example:

```bash
john --format=raw-sha512 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Example:

```bash
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt ntlm.txt
```

---

# Single Crack Mode

Generate password guesses using user information.

```bash
john --single hashes.txt
```

Example:

```bash
john --single --format=raw-md5 hashes.txt
```

---

# Custom Rules

Use your own password mutation rules.

```bash
john --rules=<RuleName> hashes.txt
```

Example:

```bash
john --rules=PoloPassword hashes.txt
```

---

# Show Cracked Passwords

Display recovered passwords without cracking again.

```bash
john --show hashes.txt
```

---

# List Supported Formats

Display every hash format supported by John.

```bash
john --list=formats
```

Search for a specific format.

```bash
john --list=formats | grep -i md5
```

---

# Linux Password Cracking

Combine passwd and shadow.

```bash
unshadow passwd shadow > unshadowed.txt
```

Crack passwords.

```bash
john unshadowed.txt
```

---

# ZIP Password Cracking

Convert ZIP archive.

```bash
zip2john secure.zip > zip_hash.txt
```

Crack password.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

Extract archive.

```bash
unzip secure.zip
```

---

# RAR Password Cracking

Convert RAR archive.

```bash
rar2john secure.rar > rar_hash.txt
```

Crack password.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
```

Extract archive.

```bash
unrar x secure.rar
```

---

# SSH Private Key Cracking

Convert SSH key.

```bash
python3 /usr/share/john/ssh2john.py id_rsa > id_rsa_hash.txt
```

Crack passphrase.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```

---

# Identify Unknown Hash

Using hash-id.py

```bash
python3 hash-id.py
```

Paste the hash when prompted.

---

# Helpful Linux Commands

Current directory.

```bash
pwd
```

List files.

```bash
ls
```

Check converted hash.

```bash
head output.txt
```

Find converter location.

```bash
which zip2john
```

```bash
which rar2john
```

```bash
which john
```

---

# Common Workflows

## Crack a Normal Hash

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

---

## Crack an MD5 Hash

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

---

## Crack a SHA256 Hash

```bash
john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

---

## Crack a SHA512 Hash

```bash
john --format=raw-sha512 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

---

## Crack an NTLM Hash

```bash
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt ntlm.txt
```

---

## View Recovered Passwords

```bash
john --show hashes.txt
```

---

## Find Supported Formats

```bash
john --list=formats
```

Search specific format.

```bash
john --list=formats | grep -i sha
```

---

# Notes

- Try automatic detection first.
- If it fails, identify the hash manually and use `--format`.
- ZIP, RAR, Linux password files, and SSH keys must be converted before cracking.
- `pwd` and `ls` solve more problems than expected.
- Always use a good wordlist like `rockyou.txt`.
```
