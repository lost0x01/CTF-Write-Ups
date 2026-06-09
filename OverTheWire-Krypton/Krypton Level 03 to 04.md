# Krypton Level 03 to 04

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 3 -> 4 |
| Status | Complete |

## Objective

Recover the password for `krypton4` from a monoalphabetic substitution cipher.

## Given Access

User: `krypton3`

Password:

```text
CAESARISEASY
```

## Method

This level removes the encryption oracle and instead gives several intercepted ciphertexts (`found1`, `found2`, `found3`) plus the target ciphertext in `krypton4`.

The hints explicitly point to frequency analysis:

- `Some letters are more prevalent in English than others.`
- `"Frequency Analysis" is your friend.`

Treat the recovered texts as a single monoalphabetic substitution corpus, align the most common symbols against common English letter frequencies and word patterns, then apply the recovered substitution to the target line:

```text
KSVVW BGSJD SVSIS VXBMN YQUUK BNWCU ANMJS
```

That decrypts to the next password.

## Commands

```bash
ssh -p 2231 krypton3@krypton.labs.overthewire.org
cat /krypton/krypton3/HINT1
cat /krypton/krypton3/HINT2
cat /krypton/krypton3/krypton4
# Use frequency analysis / substitution solving on found1, found2, found3, krypton4
ssh -p 2231 krypton4@krypton.labs.overthewire.org
```

## Result

Password for `krypton4`:

```text
BRUTE
```

## Lesson

Even without direct key access, reusing one substitution alphabet across multiple English texts leaks enough structure for recovery.

## References

- https://overthewire.org/wargames/krypton/
