# Natas Level 01 to 02

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 1 -> 2 |
| Status | Complete |

## Objective

Find the next password despite the page blocking right-click.

## Given Access

User: `natas1`

Password:

```text
0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
```

## Commands

```bash
curl -s -u natas1:0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq http://natas1.natas.labs.overthewire.org/
```

## Result

Password for `natas2`:

```text
TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
```

## Lesson

Client-side restrictions do not protect source. Fetching the HTML directly bypasses browser UI tricks.

## References

- https://overthewire.org/wargames/natas/
