# Bandit Level 03 to 04

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 3 -> 4 |
| Status | Complete |

## Objective

Find a hidden file inside the `inhere` directory.

## Given Access

User: `bandit3`

Password:

```text
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

## Method

Use `ls -la` to reveal dotfiles.

## Commands

```bash
pwd
ls -la
ls -la inhere
cat inhere/...Hiding-From-You
```

## Result

Password for `bandit4`:

```text
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

## Lesson

Hidden files are not shown by plain `ls`; use `ls -a` or `ls -la`.

