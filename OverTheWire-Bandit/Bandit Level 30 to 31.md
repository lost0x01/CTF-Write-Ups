# Bandit Level 30 to 31

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 30 -> 31 |
| Status | Complete |

## Objective

Find the password stored in Git metadata rather than a normal file.

## Given Access

User: `bandit30`

Password:

```text
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

## Method

Clone the repository and inspect tags. The tag named `secret` contains the password.

## Commands

```bash
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
cd repo
git tag -n99
git show secret
```

## Result

Password for `bandit31`:

```text
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

## Lesson

Git tags can point to annotated metadata or objects that are not obvious from the working tree.

## References

- https://overthewire.org/wargames/bandit/
