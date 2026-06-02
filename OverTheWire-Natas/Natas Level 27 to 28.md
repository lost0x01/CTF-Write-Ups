# Natas Level 27 to 28

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 27 -> 28 |
| Status | Complete |

## Objective

Abuse database string truncation and trailing-space comparison.

## Given Access

User: `natas27`

Password:

```text
u3RRffXjysjgwFU6b9xa23i6prmUsYne
```

## Method

The username column is `varchar(64)`. Creating `natas28` plus 57 spaces plus `x` passes the trim check, then truncates the final `x` on insert. Logging in with `natas28` plus the spaces works because MySQL ignores trailing spaces in string comparisons, and the final data lookup trims the value back to `natas28`.

## Result

Password for `natas28`:

```text
1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj
```

## Lesson

Application validation, database truncation, and database comparison rules must agree. If they do not, identity checks can split apart.

## References

- https://overthewire.org/wargames/natas/
