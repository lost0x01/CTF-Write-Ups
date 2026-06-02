# Natas Level 31 to 32

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 31 -> 32 |
| Status | Complete |

## Objective

Use Perl CGI filehandle confusion to read the next password.

## Given Access

User: `natas31`

Password:

```text
m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y
```

## Method

The app checks `$cgi->upload('file')`, then uses `$cgi->param('file')` in `while (<$file>)`. A multipart request with a real upload plus a preceding `file=ARGV` value makes `<ARGV>` read paths supplied in the query string.

## Result

Password for `natas32`:

```text
NaIWhW2VIrKqrc7aroJVHOZvk3RQMi0B
```

## Lesson

CGI parameter APIs can return different shapes depending on context. Mixing upload checks with scalar parameter reads can expose special Perl filehandles.

## References

- https://overthewire.org/wargames/natas/
