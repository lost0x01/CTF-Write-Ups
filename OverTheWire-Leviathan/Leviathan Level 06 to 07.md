# Leviathan Level 06 to 07

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 6 -> 7 |
| Status | Complete |

## Objective

Recover the password for `leviathan7` from the setuid binary that expects a 4-digit code.

## Given Access

User: `leviathan6`

Password:

```text
szo7HDB88w
```

## Recon

The `leviathan6` binary prints `usage: %s <4 digit code>` and calls `atoi()` on the supplied argument. No direct secret is exposed by `strings`.

## Method

Rather than reverse engineer the comparison in assembly, brute force the 0000-9999 space. Pipe commands into the helper so that when the correct code spawns `/bin/sh`, the shell automatically prints `/etc/leviathan_pass/leviathan7` and exits.

## Commands

```bash
ssh -p 2223 leviathan6@leviathan.labs.overthewire.org
for i in $(seq -w 0000 9999); do
  out=$(printf 'cat /etc/leviathan_pass/leviathan7\nexit\n' | ./leviathan6 "$i" 2>/dev/null)
  if [ "$out" != "Wrong" ]; then
    echo "CODE:$i"
    printf '%s\n' "$out"
    break
  fi
done
```

## Result

Working code:

```text
7123
```

Password for `leviathan7`:

```text
qEs5Io5yM8
```

## Lesson

A small keyspace can be the simplest attack path. If the search space is only 10,000 values, brute force may be faster than static analysis.

## References

- https://overthewire.org/wargames/leviathan/
