# Bandit Level 00 to 01

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 0 -> 1 |
| Status | Complete |

## Objective

Log in as `bandit0` and find the password for `bandit1`.

## Given Access

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Initial password:

```text
bandit0
```

## Method

List the home directory and read the obvious `readme` file.

## Commands

```bash
pwd
ls -la
cat readme
```

## Result

Password for `bandit1`:

```text
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

## Lesson

Start with basic recon: current directory, file listing, then inspect readable files.

## References

- https://overthewire.org/wargames/bandit/

