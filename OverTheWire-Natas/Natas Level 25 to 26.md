# Natas Level 25 to 26

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 25 -> 26 |
| Status | Complete |

## Objective

Read the next password through a filtered local file include.

## Given Access

User: `natas25`

Password:

```text
ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws
```

## Method

The `lang` parameter is included from `language/`, and the filter only replaces `../` once. Failed traversal attempts are logged to a session-specific file with the `User-Agent` value. Poison the log with PHP, then include the log using `....//` traversal.

## Result

Password for `natas26`:

```text
cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE
```

## Lesson

Single-pass path normalization is bypassable, and logs become executable if they are reachable through an include sink.

## References

- https://overthewire.org/wargames/natas/
