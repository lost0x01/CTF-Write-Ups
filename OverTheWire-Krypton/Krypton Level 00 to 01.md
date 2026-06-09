# Krypton Level 00 to 01

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Krypton |
| Level | 0 -> 1 |
| Status | Complete |

## Objective

Recover the initial password from the level info page and log into `krypton1`.

## Method

The page provides a base64 string:

```text
S1JZUFRPTklTR1JFQVQ=
```

Decode it with `base64 -d`.

## Commands

```bash
printf 'S1JZUFRPTklTR1JFQVQ=' | base64 -d
ssh -p 2231 krypton1@krypton.labs.overthewire.org
```

## Result

Password for `krypton1`:

```text
KRYPTONISGREAT
```

## Lesson

Always check for simple encodings before assuming the first step is cryptographically interesting.

## References

- https://overthewire.org/wargames/krypton/
