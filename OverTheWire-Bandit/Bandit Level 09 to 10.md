# Bandit Level 09 to 10

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 9 -> 10 |
| Status | Complete |

## Objective

Find human-readable strings in a binary-looking file, near repeated `=` characters.

## Given Access

User: `bandit9`

Password:

```text
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

## Method

Extract printable strings and filter for marker text.

## Commands

```bash
pwd
strings data.txt | grep ===
```

## Result

Password for `bandit10`:

```text
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

## Lesson

`strings` is useful for finding readable data inside binary or noisy files.

