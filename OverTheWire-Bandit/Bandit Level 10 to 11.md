# Bandit Level 10 to 11

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 10 -> 11 |
| Status | Complete |

## Objective

Decode base64 data in `data.txt`.

## Given Access

User: `bandit10`

Password:

```text
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

## Method

Use `base64 -d` to decode the file.

## Commands

```bash
pwd
base64 -d data.txt
```

## Result

Password for `bandit11`:

```text
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

## Lesson

Recognize common encodings and use native command-line decoders.

