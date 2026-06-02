# Natas Level 33 to 34

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 33 -> 34 |
| Status | Complete |

## Objective

Trigger PHP Phar metadata deserialization to run an uploaded PHP payload.

## Given Access

User: `natas33`

Password:

```text
2v9nDlbSF7jvawaCncr5Z9kSzkmBeoCJ
```

## Method

The `Executor` destructor checks `md5_file($this->filename) == $this->signature`, then runs `php $this->filename`. Upload `shell.php`, upload a signed Phar whose metadata is a serialized `Executor` object with private properties set to `filename=shell.php` and `signature=true`, then trigger `md5_file()` with `phar://natas.phar/test.txt`.

The loose comparison succeeds because any non-empty MD5 string equals boolean `true`, and the deserialized object's destructor executes the shell.

## Result

Password for `natas34`:

```text
j4O7Q7Q5er5XFRCepmyXJaWCSIrslCJY
```

## Lesson

PHP file functions can trigger Phar metadata deserialization. Loose comparisons and magic methods make that especially dangerous.

## References

- https://overthewire.org/wargames/natas/
