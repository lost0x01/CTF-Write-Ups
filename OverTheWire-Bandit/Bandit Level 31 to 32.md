# Bandit Level 31 to 32

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 31 -> 32 |
| Status | Complete |

## Objective

Push a specific file to the remote Git repository.

## Given Access

User: `bandit31`

Password:

```text
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

## Recon

The README requests `key.txt` with the content `May I come in?` on branch `master`. The repository ignores `*.txt`, so the file must be force-added.

## Commands

```bash
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
cd repo
printf 'May I come in?\n' > key.txt
git add -f key.txt
git commit -m 'Add key file'
git push origin master
```

## Result

The pre-receive hook rejected the push after validation, but printed the next password:

```text
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

Password for `bandit32`:

```text
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

## Lesson

`.gitignore` affects normal staging, not Git's object model. `git add -f` stages an ignored file when the challenge explicitly requires it.

## References

- https://overthewire.org/wargames/bandit/
