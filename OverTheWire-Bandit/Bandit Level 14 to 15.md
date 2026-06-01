# Bandit Level 14 to 15

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 14 -> 15 |
| Status | Complete |

## Objective

Submit the current level password to a listening service on localhost port `30000`.

## Given Access

User: `bandit14`

Password:

```text
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

## Method

The service accepts the current password over a plain TCP connection and returns the password for the next level. `nc` is the simplest tool for sending one line of input to the service.

## Commands

```bash
echo MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS | nc localhost 30000
```

## Result

Service response:

```text
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

Password for `bandit15`:

```text
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

## Lesson

Plain TCP services can be tested directly with `nc`. For line-oriented challenge services, piping `echo` into `nc` gives a repeatable one-command solution.
