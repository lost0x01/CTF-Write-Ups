# Utumno

Source: https://overthewire.org/wargames/utumno/

Utumno is the next suggested OverTheWire track after the already-completed Behemoth run in this repo. This continuation is complete through `utumno3` and currently blocked at `utumno3 -> 4` pending further exploit work.

## Progress

| Level | Status | Write-Up |
|---|---|---|
| 0 -> 1 | Complete | [[Writeups/Utumno Level 00 to 01]] |
| 1 -> 2 | Complete | [[Writeups/Utumno Level 01 to 02]] |
| 2 -> 3 | Complete | [[Writeups/Utumno Level 02 to 03]] |
| 3 -> 4 | In Progress / Blocked | [[Writeups/Utumno Level 03 to 04]] |

## Connection Pattern

```bash
ssh -p 2227 utumno<level>@utumno.labs.overthewire.org
```

## Starting Credentials

```text
Username: utumno0
Password: utumno0
```

## Notes

- Host: `utumno.labs.overthewire.org`
- Port: `2227`
- Challenge files live under `/utumno/`
- ASLR is disabled on the host (`/proc/sys/kernel/randomize_va_space = 0`), which made fixed stack addresses practical in `utumno2`.
- `utumno0` is execute-only, so the first step depended on runtime dumping through an `LD_PRELOAD` hook rather than normal static inspection.
- `utumno1` executes bytes from directory-entry names that begin with `sh_`; filenames must therefore be created as raw bytes, not UTF-8-decoded text.

## Verified Passwords

- `utumno1`: `ytvWa6DzmL`
- `utumno2`: `RdUzprHKSm`
- `utumno3`: `h3kVKJZuid`
