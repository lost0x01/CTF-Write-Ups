# Bandit Level 29 to 30

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 29 -> 30 |
| Status | Complete |

## Objective

Find the password hidden outside the production branch.

## Given Access

User: `bandit29`

Password:

```text
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

## Method

Clone the repository, list remote branches, and search all reachable commits for password references.

## Commands

```bash
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
cd repo
git branch -a
git log --oneline --decorate --all --graph
git grep -n password $(git rev-list --all)
```

## Result

The password was present on `origin/dev`.

Password for `bandit30`:

```text
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

## Lesson

Remote branches are part of the attack surface. Checking only the current branch misses data left in development history.

## References

- https://overthewire.org/wargames/bandit/
