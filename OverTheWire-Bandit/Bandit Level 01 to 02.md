# Bandit Level 01 to 02

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 1 -> 2 |
| Status | Complete |

## Objective

Read a file named `-` in the home directory.

## Given Access

User: `bandit1`

Password:

```text
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

## Method

A filename beginning with `-` can be interpreted as a command option. Prefix it with `./` to force the shell/program to treat it as a path.

## Commands

```bash
pwd
ls -la
cat ./-
```

## Result

Password for `bandit2`:

```text
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

## Lesson

Use explicit relative paths like `./filename` when filenames look like flags.

