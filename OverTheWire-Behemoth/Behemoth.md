# Behemoth

Source: https://overthewire.org/wargames/behemoth/

Behemoth is the next OverTheWire track after the completed Narnia run in this repo. This run is now complete through `behemoth8`.

## Progress

| Level | Status | Write-Up |
|---|---|---|
| 0 -> 1 | Complete | [[Writeups/Behemoth Level 00 to 01]] |
| 1 -> 2 | Complete | [[Writeups/Behemoth Level 01 to 02]] |
| 2 -> 3 | Complete | [[Writeups/Behemoth Level 02 to 03]] |
| 3 -> 4 | Complete | [[Writeups/Behemoth Level 03 to 04]] |
| 4 -> 5 | Complete | [[Writeups/Behemoth Level 04 to 05]] |
| 5 -> 6 | Complete | [[Writeups/Behemoth Level 05 to 06]] |
| 6 -> 7 | Complete | [[Writeups/Behemoth Level 06 to 07]] |
| 7 -> 8 | Complete | [[Writeups/Behemoth Level 07 to 08]] |
| 8 | Complete | [[Writeups/Behemoth Level 08 Completion]] |

## Connection Pattern

```bash
ssh -p 2221 behemoth<level>@behemoth.labs.overthewire.org
```

## Starting Credentials

```text
Username: behemoth0
Password: behemoth0
```

## Notes

- Host: `behemoth.labs.overthewire.org`
- Port: `2221`
- Challenge files live under `/behemoth/`
- The track mixes simple reversing, temp-file abuse, format strings, shellcode staging, and classic stack overflows.
- The `behemoth7 -> 8` solve depended on a reliable post-filter overflow: only the first 512 bytes were alpha-checked, but `strcpy()` still copied the trailing raw return address, NOP sled, and shellcode.

## Verified Passwords

- `behemoth1`: `8YpAQCAuKf`
- `behemoth2`: `IxPJbQtH8q`
- `behemoth3`: `JQ6tZGqt0i`
- `behemoth4`: `hpjUdlG723`
- `behemoth5`: `mVfC4rBKZ4`
- `behemoth6`: `j9I1wHzfVC`
- `behemoth7`: `sV17oOQTKc`
- `behemoth8`: `8yWcelJd0D`
