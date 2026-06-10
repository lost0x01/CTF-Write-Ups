# Narnia

Source: https://overthewire.org/wargames/narnia/

Narnia is the next OverTheWire track after the already-completed Bandit/Leviathan/Natas/Krypton set in this repo. This run is now complete through `narnia9`.

## Progress

| Level | Status | Write-Up |
|---|---|---|
| 0 -> 1 | Complete | [[Writeups/Narnia Level 00 to 01]] |
| 1 -> 2 | Complete | [[Writeups/Narnia Level 01 to 02]] |
| 2 -> 3 | Complete | [[Writeups/Narnia Level 02 to 03]] |
| 3 -> 4 | Complete | [[Writeups/Narnia Level 03 to 04]] |
| 4 -> 5 | Complete | [[Writeups/Narnia Level 04 to 05]] |
| 5 -> 6 | Complete | [[Writeups/Narnia Level 05 to 06]] |
| 6 -> 7 | Complete | [[Writeups/Narnia Level 06 to 07]] |
| 7 -> 8 | Complete | [[Writeups/Narnia Level 07 to 08]] |
| 8 -> 9 | Complete | [[Writeups/Narnia Level 08 to 09]] |
| 9 | Complete | [[Writeups/Narnia Level 09 Completion]] |

## Connection Pattern

```bash
ssh -p 2226 narnia<level>@narnia.labs.overthewire.org
```

## Starting Credentials

```text
Username: narnia0
Password: narnia0
```

## Notes

- Host: `narnia.labs.overthewire.org`
- Port: `2226`
- Challenge files live under `/narnia/`
- This host is 32-bit oriented and the track focuses on basic binary exploitation.
- The final `narnia8 -> 9` solve required preserving the live `blah` pointer and using a `setreuid(14009,14009)` prelude so the shell kept `narnia9` privileges.

## Verified Passwords

- `narnia1`: `WDcYUTG5ul`
- `narnia2`: `5agRAXeBdG`
- `narnia3`: `2xszzNl6uG`
- `narnia4`: `iqNWNk173q`
- `narnia5`: `Ni3xHPEuuw`
- `narnia6`: `BNSjoSDeGL`
- `narnia7`: `54RtepCEU0`
- `narnia8`: `i1SQ81fkb8`
- `narnia9`: `1FFD4HnU4K`
