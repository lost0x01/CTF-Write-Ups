# Leviathan

Source: https://overthewire.org/wargames/leviathan/

Leviathan is one of the OverTheWire tracks suggested after Bandit. This repo now includes a complete run through the full Leviathan sequence.

## Progress

| Level | Status | Write-Up |
|---|---|---|
| 0 -> 1 | Complete | [[Writeups/Leviathan Level 00 to 01]] |
| 1 -> 2 | Complete | [[Writeups/Leviathan Level 01 to 02]] |
| 2 -> 3 | Complete | [[Writeups/Leviathan Level 02 to 03]] |
| 3 -> 4 | Complete | [[Writeups/Leviathan Level 03 to 04]] |
| 4 -> 5 | Complete | [[Writeups/Leviathan Level 04 to 05]] |
| 5 -> 6 | Complete | [[Writeups/Leviathan Level 05 to 06]] |
| 6 -> 7 | Complete | [[Writeups/Leviathan Level 06 to 07]] |
| 7 | Complete | [[Writeups/Leviathan Level 07 Completion]] |

## Connection Pattern

```bash
ssh -p 2223 leviathan<level>@leviathan.labs.overthewire.org
```

Level 0 credentials:

```text
Username: leviathan0
Password: leviathan0
```

## Notes

- Host: `leviathan.labs.overthewire.org`
- Port: `2223`
- Passwords for each level live under `/etc/leviathan_pass/` on the target host.

## Completion

Leviathan is complete through `leviathan7`.

Final level password recovered for `leviathan7`:

```text
qEs5Io5yM8
```
