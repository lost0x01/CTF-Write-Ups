# Natas Level 08 to 09

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 8 -> 9 |
| Status | Complete |

## Objective

Reverse the custom secret encoding function and submit the original secret.

## Given Access

User: `natas8`

Password:

```text
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
```

## Method

The source shows the secret is transformed with `base64_encode`, then `strrev`, then `bin2hex`. Reverse that chain by decoding hex, reversing the string, and base64-decoding it.

## Commands

```bash
secret=$(printf '3d3d516343746d4d6d6c315669563362' | xxd -r -p | rev | base64 -d)
printf 'secret=%s\n' "$secret"

curl -s -u natas8:xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q \
  -d "secret=$secret&submit=Submit" \
  http://natas8.natas.labs.overthewire.org/
```

## Result

Decoded secret:

```text
oubWYf2kBq
```

Password for `natas9`:

```text
ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
```

## Lesson

Encoding is reversible when the full transformation chain is visible. Work backward in the exact inverse order.

## References

- https://overthewire.org/wargames/natas/
