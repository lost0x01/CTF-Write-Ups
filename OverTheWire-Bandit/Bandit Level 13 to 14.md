# Bandit Level 13 to 14

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 13 -> 14 |
| Status | Complete |

## Objective

Use a provided SSH private key to access `bandit14` and read the next password.

## Given Access

User: `bandit13`

Password:

```text
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

## Method

The home directory contains `sshkey.private`, a private key readable by `bandit13`. Because SSH back to port `2220` from localhost is blocked by the game host, the key was copied to the local artifacts folder, permissions were restricted, and it was used from the local machine to authenticate as `bandit14`.

Local artifact:

```text
05 Security Research/CTF/Over The Wire/Bandit/Artifacts/bandit14_sshkey.private
```

## Commands

On `bandit13`:

```bash
ls -la
file sshkey.private
cat sshkey.private
```

Locally:

```bash
chmod 600 "05 Security Research/CTF/Over The Wire/Bandit/Artifacts/bandit14_sshkey.private"
ssh -i "05 Security Research/CTF/Over The Wire/Bandit/Artifacts/bandit14_sshkey.private" -p 2220 bandit14@bandit.labs.overthewire.org "cat /etc/bandit_pass/bandit14"
```

## Result

Password for `bandit14`:

```text
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

## Lesson

SSH keys are authentication material and need strict file permissions. When the expected in-host connection path is blocked, use the key from a client outside the restricted host.
