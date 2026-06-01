# Bandit Level 19 to 20

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 19 -> 20 |
| Status | Complete |

## Objective

Use the provided setuid helper to read the password for `bandit20`.

## Given Access

User: `bandit19`

Password:

```text
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

## Method

The binary `bandit20-do` is owned by `bandit20` and has the setuid bit set. Running a command through it executes with `bandit20` privileges, allowing the password file to be read.

## Commands

```bash
ls -la
./bandit20-do cat /etc/bandit_pass/bandit20
```

## Result

Password for `bandit20`:

```text
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

## Lesson

Setuid binaries execute with the file owner's effective privileges. Always inspect ownership and mode bits before deciding how a helper program can be used.
