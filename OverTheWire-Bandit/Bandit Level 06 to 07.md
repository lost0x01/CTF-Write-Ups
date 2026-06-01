# Bandit Level 06 to 07

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 6 -> 7 |
| Status | Complete |

## Objective

Find a file somewhere on the server owned by `bandit7`, grouped as `bandit6`, and 33 bytes in size.

## Given Access

User: `bandit6`

Password:

```text
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## Method

Search from `/` and suppress permission errors.

## Commands

```bash
pwd
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat $(find / -user bandit7 -group bandit6 -size 33c 2>/dev/null)
```

## Result

Password for `bandit7`:

```text
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

## Lesson

Redirect noisy errors with `2>/dev/null` when searching across protected filesystem paths.

