# Bandit Level 25 to 26

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 25 -> 26 |
| Status | Complete |

## Objective

Use the provided SSH key to access `bandit26`, whose login shell is intentionally restricted.

## Given Access

User: `bandit25`

Password:

```text
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

## Recon

The home directory contains `bandit26.sshkey`. The `bandit26` account uses `/usr/bin/showtext` as its shell, which opens text through `more`.

## Method

Connect with the SSH key in a very short terminal so `more` pauses. Press `v` to open the text in `vim`, then use `vim` to read `/etc/bandit_pass/bandit26`.

## Commands

```bash
ls -la
cat bandit26.sshkey
ssh -i bandit26.sshkey -p 2220 bandit26@bandit.labs.overthewire.org

# In the paused more session:
v

# In vim:
:e /etc/bandit_pass/bandit26
```

## Result

Password for `bandit26`:

```text
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

## Lesson

Restricted login shells can still expose escape paths through pagers and editors. Terminal size mattered because `more` only became interactive when output paused.

## References

- https://overthewire.org/wargames/bandit/
