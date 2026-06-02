# Natas Level 32 to 33

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 32 -> 33 |
| Status | Complete |

## Objective

Prove command execution through the same Perl CGI `ARGV` primitive.

## Given Access

User: `natas32`

Password:

```text
NaIWhW2VIrKqrc7aroJVHOZvk3RQMi0B
```

## Method

Use the upload plus `file=ARGV` trick again, but put a command ending in `|` in the query string. Listing the webroot revealed a setuid helper named `getpassword`; executing it returned the next password.

Command:

```text
./getpassword |
```

## Result

Password for `natas33`:

```text
2v9nDlbSF7jvawaCncr5Z9kSzkmBeoCJ
```

## Lesson

The `ARGV` filehandle primitive can be upgraded from file read to command execution when the supplied argument is a shell pipe.

## References

- https://overthewire.org/wargames/natas/
