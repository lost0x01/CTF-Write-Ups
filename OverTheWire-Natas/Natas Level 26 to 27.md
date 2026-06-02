# Natas Level 26 to 27

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 26 -> 27 |
| Status | Complete |

## Objective

Exploit unsafe PHP object deserialization.

## Given Access

User: `natas26`

Password:

```text
cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE
```

## Method

The `drawing` cookie is base64-decoded and unserialized. The `Logger` destructor writes `$exitMsg` to `$logFile`, so a serialized `Logger` object can write a PHP payload into `img/` and then execute it through the web server.

## Result

Password for `natas27`:

```text
u3RRffXjysjgwFU6b9xa23i6prmUsYne
```

## Lesson

Never unserialize attacker-controlled data. Magic methods such as destructors are common POP-chain execution points.

## References

- https://overthewire.org/wargames/natas/
