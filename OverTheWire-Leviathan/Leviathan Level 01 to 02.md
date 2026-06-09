# Leviathan Level 01 to 02

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 1 -> 2 |
| Status | Complete |

## Objective

Recover the password for `leviathan2` by abusing the setuid helper in `leviathan1`.

## Given Access

User: `leviathan1`

Password:

```text
3QJ3TgzHDq
```

## Recon

The home directory contains a setuid binary named `check`.

## Method

`strings` hinted at the values `sex`, `love`, and `secr`, and `ltrace` confirmed the binary compares user input against `sex` with `strcmp()`.

Submitting the correct password causes the program to spawn `/bin/sh` with effective user `leviathan2`. From that shell, read `/etc/leviathan_pass/leviathan2`.

## Commands

```bash
ssh -p 2223 leviathan1@leviathan.labs.overthewire.org
strings -a check
ltrace ./check
./check
# enter: sex
whoami
cat /etc/leviathan_pass/leviathan2
```

## Result

Password for `leviathan2`:

```text
NsN1HwFoyN
```

## Lesson

Dynamic tracing is often the fastest path through authentication wrappers. When a binary uses `strcmp()` on user-controlled input, `ltrace` can expose the exact secret without full reverse engineering.

## References

- https://overthewire.org/wargames/leviathan/
