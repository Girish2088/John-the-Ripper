# John the Ripper Cheat Sheet

A quick revision sheet for the John the Ripper commands I use most often.

---

# Basic Syntax

```bash
john [options] <target>
```

---

# Basic Hash Cracking

Automatically detect the hash format.

```bash
john hashes.txt
```

---

# Dictionary Attack

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

---

# Specify Hash Format

```bash
john --format=<format> --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

Common Formats:

| Format | Used For |
|---------|----------|
| `raw-md5` | MD5 |
| `raw-sha256` | SHA256 |
| `raw-sha512` | SHA512 |
| `NT` | NTLM |

---

# Single Crack Mode

Generate password guesses using user information.

```bash
john --single hashes.txt
```

---

# Custom Rules

```bash
john --rules=<RuleName> hashes.txt
```

Example:

```bash
john --rules=PoloPassword hashes.txt
```

---

# Show Cracked Passwords

```bash
john --show hashes.txt
```

---

# List Supported Formats

```bash
john --list=formats
```

Search for a specific format:

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

Convert archive.

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

```bash
python3 hash-id.py
```

---

# Useful Linux Commands

Current directory:

```bash
pwd
```

List files:

```bash
ls
```

View converted hash:

```bash
head output.txt
```

Find tool location:

```bash
which john
which zip2john
which rar2john
```

---

# Common Workflow

```text
Target

↓

Need Conversion?
│
├── No
│     ↓
│   John
│
└── Yes
      ↓
Converter
(zip2john / rar2john / ssh2john / unshadow)
      ↓
John-Compatible Hash
      ↓
John
      ↓
Password Found
```

---

# Common Converter Tools

| Target | Converter |
|---------|-----------|
| Linux Passwords | `unshadow` |
| ZIP Archive | `zip2john` |
| RAR Archive | `rar2john` |
| SSH Private Key | `ssh2john.py` |

---

# Things to Remember

- Start with automatic hash detection.
- If it fails, specify `--format`.
- ZIP, RAR, SSH Keys and Linux password files must be converted first.
- A wrong format usually means no password will be found.
- `rockyou.txt` is the most commonly used wordlist.
- If something isn't working, check:
  - `pwd`
  - `ls`
  - File paths
  - Conversion output

---

# John vs Hashcat

| John the Ripper | Hashcat |
|-----------------|----------|
| Easier to use | Faster (especially with GPU) |
| Can auto-detect many formats | Usually requires `-m` |
| Uses helper converters | Optimized for performance |
| Great for Linux password files | Great for large password audits |
```
