# Bandit Level 02 to 03

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 2 -> 3 |
| Status | Complete |

## Objective

Read a file whose name contains spaces and leading dashes.

## Given Access

User: `bandit2`

Password:

```text
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

## Method

Escape spaces and use `./` so the filename is interpreted as a path.

## Commands

```bash
pwd
ls -la
cat ./--spaces\ in\ this\ filename--
```

## Result

Password for `bandit3`:

```text
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

## Lesson

Shell metacharacters and whitespace matter. Quote or escape filenames exactly.

