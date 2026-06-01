# Bandit Level 07 to 08

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 7 -> 8 |
| Status | Complete |

## Objective

Find the password next to the word `millionth` in `data.txt`.

## Given Access

User: `bandit7`

Password:

```text
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

## Method

Search the file for the target keyword.

## Commands

```bash
pwd
grep millionth data.txt
```

## Result

Password for `bandit8`:

```text
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

## Lesson

`grep` is the fastest first move when the target text pattern is known.

