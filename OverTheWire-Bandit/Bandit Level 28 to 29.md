# Bandit Level 28 to 29

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 28 -> 29 |
| Status | Complete |

## Objective

Recover a password that was removed from a Git repository.

## Given Access

User: `bandit28`

Password:

```text
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

## Method

The current README has the password replaced with `xxxxxxxxxx`. Inspect the Git history and patch diffs to recover the earlier value.

## Commands

```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
cd repo
cat README.md
git log --oneline
git log -p -- README.md
```

## Result

Password for `bandit29`:

```text
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

## Lesson

Deleting a secret from the latest commit does not remove it from repository history.

## References

- https://overthewire.org/wargames/bandit/
