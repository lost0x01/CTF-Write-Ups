# Bandit Level 32 to 33

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 32 -> 33 |
| Status | Complete |

## Objective

Escape the uppercase-only shell and read the final Bandit password.

## Given Access

User: `bandit32`

Password:

```text
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

## Method

The uppercase shell transforms normal commands to uppercase, but shell variables are expanded first. Running `$0` invokes the current shell path and drops into a normal shell.

## Commands

```bash
$0
whoami
cat /etc/bandit_pass/bandit33
```

## Result

Password for `bandit33`:

```text
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```

Logging in as `bandit33` shows the final README:

```text
Congratulations on solving the last level of this game!
```

## Lesson

Input filters that transform command text can still be bypassed through shell expansion semantics.

## References

- https://overthewire.org/wargames/bandit/
