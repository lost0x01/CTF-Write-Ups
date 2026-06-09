# Krypton Level 02 to 03

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 2 -> 3 |
| Status | Complete |

## Objective

Recover the password for `krypton3` using the Caesar-cipher encryption oracle.

## Given Access

User: `krypton2`

Password:

```text
ROTTEN
```

## Method

The ciphertext in `krypton3` is:

```text
OMQEMDUEQMEK
```

Because `/krypton/krypton2/encrypt` lets you encrypt chosen plaintext, feed it a single `A` from a writable temp directory containing a symlink to `keyfile.dat`. The result is `M`, which means plaintext `A` is shifted to `M` — a Caesar shift of 12.

Decrypting `OMQEMDUEQMEK` by shifting back 12 yields `CAESARISEASY`.

## Commands

```bash
ssh -p 2231 krypton2@krypton.labs.overthewire.org
cat /krypton/krypton2/krypton3
tmp=$(mktemp -d)
chmod 777 "$tmp"
cd "$tmp"
ln -s /krypton/krypton2/keyfile.dat
printf A > plain
/krypton/krypton2/encrypt plain
cat ciphertext
```

## Result

Password for `krypton3`:

```text
CAESARISEASY
```

## Lesson

Chosen-plaintext access collapses a Caesar cipher immediately. One character is enough to reveal the entire shift.

## References

- https://overthewire.org/wargames/krypton/
