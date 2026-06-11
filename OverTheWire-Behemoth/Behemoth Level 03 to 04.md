# Behemoth Level 03 to 04

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Behemoth |
| Level | 3 -> 4 |
| Status | Complete |

## Objective

Use the format string in `behemoth3` to redirect control flow into shellcode and spawn a shell as `behemoth4`.

## Given Access

User: `behemoth3`

Password:

```text
JQ6tZGqt0i
```

## Recon

The binary passes attacker-controlled input directly to `printf()`. The verified target on this host was `puts@got = 0x0804b218`.

A direct environment-variable shellcode injection through shell/Python plumbing was unreliable because some high bytes were mangled. A compiled wrapper that installed a raw-byte environment string in-process was the reliable path.

## Method

1. Compile a tiny wrapper that sets a static `EGG=` environment variable containing raw shellcode bytes and then execs `/behemoth/behemoth3`.
2. Overwrite `puts@got` in two half-word writes using an addresses-first payload and `%1$hn` / `%2$hn`.
3. Aim the overwrite into the NOP sled at the verified working jump target `0xffffdd20`.
4. Once `puts()` resolves into shellcode, read the next password from the resulting `behemoth4` shell.

## Commands

```bash
ssh -p 2221 behemoth3@behemoth.labs.overthewire.org
objdump -R /behemoth/behemoth3 | grep puts
# verified target: puts@got = 0x0804b218
# use a compiled wrapper to install the raw-byte EGG environment reliably
# then feed a format payload that writes 0xffffdd20 into puts@got with %1$hn / %2$hn
```

## Result

Password for `behemoth4`:

```text
hpjUdlG723
```

## Lesson

For format-string GOT overwrites, preserve the exact target address, argument positions, and the byte-clean shellcode staging method that actually worked.

## References

- https://overthewire.org/wargames/behemoth/
