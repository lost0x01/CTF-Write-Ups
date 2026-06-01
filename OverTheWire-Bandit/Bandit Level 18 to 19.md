# Bandit Level 18 to 19

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 18 -> 19 |
| Status | Complete |

## Objective

Recover the next password even though the remote shell logs out immediately.

## Given Access

User: `bandit18`

Password:

```text
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

## Method

The interactive shell exits immediately, but SSH can still run a command directly. Passing `cat readme` as the remote command reads the file before the session closes.

## Commands

```bash
ssh -p 2220 bandit18@bandit.labs.overthewire.org "cat readme"
```

## Result

Password for `bandit19`:

```text
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

## Lesson

When a login shell is restricted or exits immediately, direct remote command execution through SSH may still work.
