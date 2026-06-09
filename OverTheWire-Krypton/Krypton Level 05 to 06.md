# Krypton Level 05 to 06

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 5 -> 6 |
| Status | Complete |

## Objective

Recover the password for `krypton6` from a Vigenère cipher with unknown key length.

## Given Access

User: `krypton5`

Password:

```text
CLEARTEXT
```

## Method

The ciphertext in `krypton6` is:

```text
BELOS Z
```

This level again provides several longer ciphertext samples, but no key length. Determine the likely key length first from repeated-pattern spacing / index-of-coincidence style analysis, then solve the resulting Vigenère columns with frequency analysis.

The recovered key is `KEYLENGTH`, which decrypts `BELOS Z` to `RANDOM`.

## Commands

```bash
ssh -p 2231 krypton5@krypton.labs.overthewire.org
cat /krypton/krypton5/found1
cat /krypton/krypton5/found2
cat /krypton/krypton5/found3
cat /krypton/krypton5/krypton6
# Determine key length, recover key KEYLENGTH, decrypt target
ssh -p 2231 krypton6@krypton.labs.overthewire.org
```

## Result

Password for `krypton6`:

```text
RANDOM
```

## Lesson

Unknown-key-length Vigenère is still weak when enough English ciphertext is available. Repetition statistics reveal the period, and then standard frequency analysis finishes the job.

## References

- https://overthewire.org/wargames/krypton/
