# Bandit Level 17 to 18

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 17 -> 18 |
| Status | Complete |

## Objective

Find the changed password by comparing `passwords.old` and `passwords.new`.

## Given Access

User: `bandit17`

Authentication:

```text
05 Security Research/CTF/Over The Wire/Bandit/Artifacts/bandit17_sshkey.private
```

## Method

Use `diff` to compare the two files. The new line in `passwords.new` is the next password.

## Commands

```bash
ssh -i "05 Security Research/CTF/Over The Wire/Bandit/Artifacts/bandit17_sshkey.private" -p 2220 bandit17@bandit.labs.overthewire.org "diff passwords.old passwords.new"
```

## Result

Diff output:

```text
42c42
< 390zFj2NETFVZkqYw8UEFdN6h40oGVtT
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

Password for `bandit18`:

```text
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

## Lesson

`diff` is ideal when the answer is one changed line among many. The line marked with `>` came from the newer file.
