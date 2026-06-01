# Bandit Level 11 to 12

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 11 -> 12 |
| Status | Complete |

## Objective

Decode text rotated by 13 characters.

## Given Access

User: `bandit11`

Password:

```text
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

## Method

Apply ROT13 with `tr`. The important detail is mapping uppercase and lowercase ranges correctly.

## Commands

```bash
pwd
cat data.txt
cat data.txt | tr "A-Za-z" "N-ZA-Mn-za-m"
```

## Result

Password for `bandit12`:

```text
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

## Lesson

`tr` can perform substitution ciphers when source and destination alphabets are specified correctly.

