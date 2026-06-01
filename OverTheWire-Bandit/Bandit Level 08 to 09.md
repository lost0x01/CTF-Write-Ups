# Bandit Level 08 to 09

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 8 -> 9 |
| Status | Complete |

## Objective

Find the only line in `data.txt` that occurs once.

## Given Access

User: `bandit8`

Password:

```text
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

## Method

Sort the file first, then use `uniq -u` to show only unique lines.

## Commands

```bash
pwd
sort data.txt | uniq -u
```

## Result

Password for `bandit9`:

```text
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

## Lesson

`uniq` only detects adjacent duplicates, so sort before using it on unsorted data.

