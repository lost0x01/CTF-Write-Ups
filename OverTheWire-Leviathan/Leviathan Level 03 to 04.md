# Leviathan Level 03 to 04

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 3 -> 4 |
| Status | Complete |

## Objective

Recover the password for `leviathan4` from the setuid binary in `leviathan3`.

## Given Access

User: `leviathan3`

Password:

```text
f0n8h2iWLP
```

## Recon

The account contains a setuid program named `level3`. Running `strings` showed several suspicious strings, and `ltrace` revealed the real password comparison.

## Method

`ltrace ./level3` shows the binary calling:

```text
strcmp("foo\n", "snlprintf\n")
```

So the correct password is `snlprintf`. Entering that value drops into a shell running as `leviathan4`, which can then read the next password file.

## Commands

```bash
ssh -p 2223 leviathan3@leviathan.labs.overthewire.org
ltrace ./level3
./level3
# enter: snlprintf
whoami
cat /etc/leviathan_pass/leviathan4
```

## Result

Password for `leviathan4`:

```text
WG1egElCvO
```

## Lesson

When tracing a stripped or unfamiliar binary, follow the library calls first. A single `strcmp()` often exposes the entire decision point.

## References

- https://overthewire.org/wargames/leviathan/
