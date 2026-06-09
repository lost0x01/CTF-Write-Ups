# Krypton Level 01 to 02

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 1 -> 2 |
| Status | Complete |

## Objective

Recover the password for `krypton2` from the ciphertext in `/krypton/krypton1/krypton2`.

## Given Access

User: `krypton1`

Password:

```text
KRYPTONISGREAT
```

## Method

Read the file:

```text
YRIRY GJB CNFFJBEQ EBGGRA
```

This is ROT13. Decoding it yields the phrase `LEVEL TWO PASSWORD ROTTEN`, so the next password is `ROTTEN`.

## Commands

```bash
ssh -p 2231 krypton1@krypton.labs.overthewire.org
cat /krypton/krypton1/krypton2
printf 'YRIRY GJB CNFFJBEQ EBGGRA' | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

## Result

Password for `krypton2`:

```text
ROTTEN
```

## Lesson

If a challenge says “simple rotation,” try ROT13 first before doing anything more elaborate.

## References

- https://overthewire.org/wargames/krypton/
