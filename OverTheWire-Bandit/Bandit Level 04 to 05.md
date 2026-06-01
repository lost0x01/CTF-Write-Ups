# Bandit Level 04 to 05

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 4 -> 5 |
| Status | Complete |

## Objective

Find the only human-readable file in `inhere`.

## Given Access

User: `bandit4`

Password:

```text
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

## Method

Use `file` to identify file types, then read the ASCII text file.

## Commands

```bash
pwd
find inhere -type f -exec file {} \;
cat inhere/-file07
```

## Result

Password for `bandit5`:

```text
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

## Lesson

`file` is useful when names are misleading and content type matters.

