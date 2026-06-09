# Krypton

Source: https://overthewire.org/wargames/krypton/

Krypton is one of the OverTheWire tracks suggested after Bandit. This repo now includes a complete run through the full Krypton sequence.

## Progress

| Level | Status | Write-Up |
|---|---|---|
| 0 -> 1 | Complete | [[Writeups/Krypton Level 00 to 01]] |
| 1 -> 2 | Complete | [[Writeups/Krypton Level 01 to 02]] |
| 2 -> 3 | Complete | [[Writeups/Krypton Level 02 to 03]] |
| 3 -> 4 | Complete | [[Writeups/Krypton Level 03 to 04]] |
| 4 -> 5 | Complete | [[Writeups/Krypton Level 04 to 05]] |
| 5 -> 6 | Complete | [[Writeups/Krypton Level 05 to 06]] |
| 6 -> 7 | Complete | [[Writeups/Krypton Level 06 to 07]] |
| 7 | Complete | [[Writeups/Krypton Level 07 Completion]] |

## Connection Pattern

```bash
ssh -p 2231 krypton<level>@krypton.labs.overthewire.org
```

## Starting Credentials

The level 0 page provides a base64-encoded string:

```text
S1JZUFRPTklTR1JFQVQ=
```

Decoded level 1 password:

```text
KRYPTONISGREAT
```

## Notes

- Host: `krypton.labs.overthewire.org`
- Port: `2231`
- Challenge files live under `/krypton/`

## Completion

Krypton is complete through `krypton7`.

Final level password recovered for `krypton7`:

```text
LFSRISNOTRANDOM
```
