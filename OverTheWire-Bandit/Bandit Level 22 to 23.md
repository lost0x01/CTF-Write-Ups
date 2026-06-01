# Bandit Level 22 to 23

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 22 -> 23 |
| Status | Complete |

## Objective

Use the `bandit23` cron script logic to derive the temporary file path containing the next password.

## Given Access

User: `bandit22`

Password:

```text
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

## Method

The cron script computes a filename from the executing username. Since the cron job runs as `bandit23`, reproduce the same hash calculation with `bandit23` as the name, then read the generated file from `/tmp`.

## Commands

```bash
cat /etc/cron.d/cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh
mytarget=$(echo I am user bandit23 | md5sum | cut -d " " -f 1)
echo "$mytarget"
cat /tmp/$mytarget
```

## Result

Computed target:

```text
8ca319486bfbbc3663ea0fbe81326349
```

Password for `bandit23`:

```text
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

## Lesson

When a script derives a path from runtime context, reproduce that context intentionally. Here, substituting `bandit23` for `whoami` reveals the cron-created file.
