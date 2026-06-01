# Bandit Level 05 to 06

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 5 -> 6 |
| Status | Complete |

## Objective

Find a file that is human-readable, 1033 bytes, and not executable.

## Given Access

User: `bandit5`

Password:

```text
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

## Method

Use `find` predicates for size and executable status.

## Commands

```bash
pwd
find inhere -type f -size 1033c ! -executable -exec file {} \;
cat $(find inhere -type f -size 1033c ! -executable)
```

## Result

Password for `bandit6`:

```text
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## Lesson

`find` can combine constraints like type, size, permissions, and execution bits.

