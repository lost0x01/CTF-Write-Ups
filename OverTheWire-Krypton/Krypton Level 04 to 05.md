# Krypton Level 04 to 05

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 4 -> 5 |
| Status | Complete |

## Objective

Recover the password for `krypton5` from a Vigenère cipher with known key length 6.

## Given Access

User: `krypton4`

Password:

```text
BRUTE
```

## Method

The target ciphertext in `krypton5` is:

```text
HCIKV RJOX
```

The level gives two longer English ciphertexts and tells you the Vigenère key length is 6. Split the ciphertext streams into 6 columns by position, perform frequency analysis on each column as a Caesar-shifted stream, recover the six-letter key, then decrypt the target.

Applying that process yields the plaintext password `CLEARTEXT`.

## Commands

```bash
ssh -p 2231 krypton4@krypton.labs.overthewire.org
cat /krypton/krypton4/found1
cat /krypton/krypton4/found2
cat /krypton/krypton4/krypton5
# Solve as Vigenère with key length 6
ssh -p 2231 krypton5@krypton.labs.overthewire.org
```

## Result

Password for `krypton5`:

```text
CLEARTEXT
```

## Lesson

Once the key length of a Vigenère cipher is known, the problem reduces to several independent Caesar ciphers.

## References

- https://overthewire.org/wargames/krypton/
