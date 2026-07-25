# John the Ripper

John the Ripper (JtR) is an **offline password cracking tool**.

It is used to recover passwords from:

- Password Hashes
- Linux Password Files
- Windows Password Hashes
- ZIP Archives
- RAR Archives
- SSH Private Keys

Unlike online attacks (like Hydra), John works on files that you already have.

---

# Where John Fits

```
Password
    │
    ▼
Hash Function
    │
    ▼
Hash
    │
    ▼
John the Ripper
    │
    ▼
Recovered Password
```

John doesn't hack into a server.

It tries to recover the original password from an existing hash or password-protected file.

---

# How John Works

Every attack follows the same workflow.

```
Target
      │
      ▼
Prepare Target
(Convert if needed)
      │
      ▼
John
      │
      ▼
Generate Password Guess
      │
      ▼
Hash Guess
      │
      ▼
Compare
      │
      ▼
Match?
      │
      ├── Yes
      │      │
      │      ▼
      │ Password Found
      │
      └── No
             │
             ▼
       Try Next Password
```

No matter whether the target is a ZIP file, Linux password file, or SSH key, the workflow is almost the same.

---

# John Can Crack

### Password Hashes

```
hash.txt

↓

john

↓

Password
```

---

### Linux Passwords

```
passwd
+
shadow

↓

unshadow

↓

john

↓

Password
```

---

### ZIP Files

```
secure.zip

↓

zip2john

↓

ZIP Hash

↓

john

↓

Password
```

---

### RAR Files

```
secure.rar

↓

rar2john

↓

RAR Hash

↓

john

↓

Password
```

---

### SSH Private Keys

```
id_rsa

↓

ssh2john.py

↓

SSH Hash

↓

john

↓

Passphrase
```

---

# Converter Tools

Some files cannot be cracked directly.

They must first be converted into a format that John understands.

| Original File | Converter |
|--------------|-----------|
| Linux Password Files | `unshadow` |
| ZIP Archive | `zip2john` |
| RAR Archive | `rar2john` |
| SSH Private Key | `ssh2john.py` |

Think of these tools as translators.

```
Original File

↓

Converter

↓

John-Compatible Hash

↓

John
```

---

# Automatic Hash Detection

John tries to identify the hash format automatically.

Most of the time it works.

Sometimes it doesn't.

Example:

```
Hash

↓

John guesses format

↓

Correct?

↓

Yes → Password Found

No → Specify Format Manually
```

So don't blindly trust automatic detection.

---

# Format-Specific Cracking

If John cannot detect the correct hash type, we tell it manually.

Example:

```
Raw MD5

↓

--format=raw-md5
```

The correct format is important.

Wrong format means John will never find the password.

---

# Single Crack Mode

Normally John uses a wordlist.

Single Crack Mode is different.

It creates password guesses using information about the user.

Example:

Username:

```
joker
```

John may try:

```
joker
joker1
joker123
Joker!
j0ker
```

Sometimes this is much faster than using a huge wordlist.

---

# Custom Rules

People usually don't create completely random passwords.

Example:

```
password
```

becomes

```
Password
Password1
Password123
Password!
```

John can automatically generate these variations using **Rules**.

This increases the chance of recovering the password.

---

# Windows Passwords

Windows stores password hashes inside:

```
SAM

or

NTDS.dit
```

These usually contain **NTLM** hashes.

John can attempt to recover those passwords offline.

---

# Linux Passwords

Linux stores user information in:

```
/etc/passwd
```

Password hashes are stored separately in:

```
/etc/shadow
```

Before cracking, both files are combined using:

```
unshadow
```

Then the output is given to John.

---

# Why Hash Identification Matters

Suppose someone gives you:

```
5f4dcc3b5aa765d61d8327deb882cf99
```

John cannot always know whether it is:

- MD5
- NTLM
- MD4

Sometimes we need to identify the hash manually and then specify the correct format.

Wrong format = Wrong result.

---

# John vs Hashcat

Both are offline password cracking tools.

| John the Ripper | Hashcat |
|-----------------|----------|
| Easier to start with | Faster on powerful hardware |
| Can automatically detect many hashes | Usually requires hash mode (`-m`) |
| Uses helper tools like `zip2john`, `ssh2john` | GPU optimized |
| Great for Linux password files | Great for large password audits |

Both tools follow the same idea:

```
Guess Password

↓

Hash It

↓

Compare

↓

Password Found
```

---

# Where is John Used?

- Penetration Testing
- Digital Forensics
- Password Audits
- Incident Response
- CTF Challenges
- Security Research

---

# Advantages

- Supports many hash formats.
- Can crack ZIP, RAR, SSH keys and Linux passwords.
- Automatic hash detection.
- Supports custom rules.
- Open Source.

---

# Limitations

- Works only on files you already have.
- Automatic detection is not always correct.
- Strong passwords may not be recovered.
- Success depends on the attack method and wordlist.

---

# Troubleshooting I Learned

Most of the time, John isn't the problem.

I am 😅.

Whenever something doesn't work, I check:

```bash
pwd
```

Am I in the correct directory?

```bash
ls
```

Does the file actually exist?

If using a converter:

```bash
head output.txt
```

Did the converter create a valid hash?

Most errors I've faced were because of:

- Wrong file path
- Wrong working directory
- Wrong hash format

Not because John was broken.

---

# Interview Questions

### What is John the Ripper?

An offline password cracking tool used to recover passwords from hashes and password-protected files.

---

### Does John decrypt hashes?

No.

It generates password guesses, hashes them, and compares them with the target hash.

---

### Why do we need converter tools?

Some files (ZIP, RAR, SSH keys, Linux password files) are not hashes.

They must first be converted into a John-compatible format.

---

### What is Single Crack Mode?

A mode where John generates password guesses using user information instead of a normal wordlist.

---

### Why is hash identification important?

Using the wrong hash format means John cannot recover the password.

---

# Memory Hook

```
Target

↓

Convert (if needed)

↓

John

↓

Guess Password

↓

Hash

↓

Compare

↓

Password Found
```

> **Think in workflows, not commands.**
>
> Whether you're cracking a hash, ZIP file, Linux password database, or SSH key, the workflow is almost always the same.
