# Bandit Level 21 to 22

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 21 -> 22 |
| Status | Complete |

## Objective

Inspect cron jobs to find where the `bandit22` password is being written.

## Given Access

User: `bandit21`

Password:

```text
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

## Method

Review `/etc/cron.d` for Bandit cron entries, then read the referenced script to identify the output file containing the next password.

## Commands

```bash
ls -la /etc/cron.d
cat /etc/cron.d/cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

## Result

The cron script writes `/etc/bandit_pass/bandit22` to:

```text
/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Password for `bandit22`:

```text
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

## Lesson

Cron jobs often expose useful execution paths. Read both the crontab entry and the script it launches.
