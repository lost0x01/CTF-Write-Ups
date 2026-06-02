# Natas Level 00 to 01

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 0 -> 1 |
| Status | Complete |

## Objective

Find the password for `natas1` in the first web page.

## Given Access

User: `natas0`

Password:

```text
natas0
```

## Commands

```bash
curl -s -u natas0:natas0 http://natas0.natas.labs.overthewire.org/
```

## Result

Password for `natas1`:

```text
0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
```

## Lesson

Always inspect page source. HTML comments are delivered to the client even when they are not visible in the rendered page.

## References

- https://overthewire.org/wargames/natas/
