# Krypton Level 06 to 07

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 6 -> 7 |
| Status | Complete |

## Objective

Recover the password for `krypton7` from the stream-cipher challenge.

## Given Access

User: `krypton6`

Password:

```text
RANDOM
```

## Recon

The level provides:

- `encrypt6` (setuid helper)
- `krypton7` ciphertext: `PNUKLYLWRQKGKBE`
- hints stating the random generator is periodic and uses an `8 bit LFSR`

## Method

Because `encrypt6` acts as an encryption oracle, create a writable temp directory, symlink `keyfile.dat`, and encrypt a known plaintext of all `A`s with the same length as the target ciphertext:

```text
AAAAAAAAAAAAAAA -> EICTDGYIYZKTHNS
```

For this alphabetic stream cipher, encrypting `A` reveals the keystream directly. Subtract that keystream from the target ciphertext:

```text
PNUKLYLWRQKGKBE
- EICTDGYIYZKTHNS
= LFSRISNOTRANDOM
```

## Commands

```bash
ssh -p 2231 krypton6@krypton.labs.overthewire.org
cat /krypton/krypton6/krypton7
tmp=$(mktemp -d)
chmod 777 "$tmp"
cd "$tmp"
ln -s /krypton/krypton6/keyfile.dat
printf AAAAAAAAAAAAAAA > p
/krypton/krypton6/encrypt6 p out
cat out
# subtract keystream from target ciphertext
ssh -p 2231 krypton7@krypton.labs.overthewire.org
```

## Result

Password for `krypton7`:

```text
LFSRISNOTRANDOM
```

## Lesson

A weak or repeating keystream destroys the security of a stream cipher. A chosen-plaintext encryption oracle makes keystream recovery trivial.

## References

- https://overthewire.org/wargames/krypton/
