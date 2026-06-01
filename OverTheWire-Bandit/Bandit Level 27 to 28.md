# Bandit Level 27 to 28

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 27 -> 28 |
| Status | Complete |

## Objective

Clone the `bandit27-git` repository and read the next password.

## Given Access

User: `bandit27`

Password:

```text
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

## Method

Clone the repository over SSH and inspect its README.

## Commands

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
cd repo
cat README
```

## Result

Password for `bandit28`:

```text
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

## Lesson

For Git-based levels, the game user and Git user differ. The SSH password is still the current Bandit password.

## References

- https://overthewire.org/wargames/bandit/
