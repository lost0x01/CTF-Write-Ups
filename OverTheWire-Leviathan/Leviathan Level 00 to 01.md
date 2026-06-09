# Leviathan Level 00 to 01

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 0 -> 1 |
| Status | Complete |

## Objective

Recover the password for `leviathan1` from the starting account.

## Given Access

User: `leviathan0`

Password:

```text
leviathan0
```

## Recon

After logging in over SSH, the home directory was mostly empty except for a hidden `.backup/` directory containing `bookmarks.html`.

## Method

Search the hidden backup file for password-related strings. A malformed bookmark entry leaks the next password directly in the `HREF` attribute.

## Commands

```bash
ssh -p 2223 leviathan0@leviathan.labs.overthewire.org
ls -la
find . -maxdepth 2 -type f | sort
grep -i -n 'leviathan\|password\|pass' .backup/bookmarks.html
ssh -p 2223 leviathan1@leviathan.labs.overthewire.org
```

## Result

The leaked bookmark entry contains the password for `leviathan1`:

```text
3QJ3TgzHDq
```

Relevant line:

```text
1049:<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is 3QJ3TgzHDq"
```

Logging in as `leviathan1` with that password succeeds.

## Lesson

Hidden files and backup artifacts are often more valuable than the obvious application surface. Grepping likely stash files for credential keywords is quick, cheap recon.

## References

- https://overthewire.org/wargames/leviathan/
