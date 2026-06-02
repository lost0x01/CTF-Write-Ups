# Natas Level 11 to 12

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 11 -> 12 |
| Status | Complete |

## Objective

Forge an XOR-encrypted cookie to set `showpassword` to `yes`.

## Given Access

User: `natas11`

Password:

```text
UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
```

## Method

The cookie is `base64_encode(xor_encrypt(json_encode($data)))`. Because the default plaintext JSON is known, XOR the decoded cookie with the known JSON to recover the repeating key, then encrypt a forged JSON object.

## Commands

```python
import base64, urllib.parse

cookie = "HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg%3D"
ct = base64.b64decode(urllib.parse.unquote(cookie))
pt = b'{"showpassword":"no","bgcolor":"#ffffff"}'
key = bytes(c ^ p for c, p in zip(ct, pt))[:4]

forge = b'{"showpassword":"yes","bgcolor":"#ffffff"}'
forged = base64.b64encode(bytes(b ^ key[i % len(key)] for i, b in enumerate(forge)))
print(key, forged.decode())
```

```bash
curl -s -u natas11:UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk \
  -b 'data=HmYkBwozJw4WNyAAFyB1VUc9MhxHaHUNAic4Awo2dVVHZzEJAyIxCUc5' \
  http://natas11.natas.labs.overthewire.org/
```

## Result

Recovered XOR key:

```text
eDWo
```

Password for `natas12`:

```text
yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB
```

## Lesson

Repeating-key XOR is broken when an attacker knows plaintext and ciphertext. Encryption without integrity also allows forged cookies.

## References

- https://overthewire.org/wargames/natas/
