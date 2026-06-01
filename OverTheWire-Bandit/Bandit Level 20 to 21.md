# Bandit Level 20 to 21

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 20 -> 21 |
| Status | Complete |

## Objective

Use `suconnect` to connect to a local listener, validate the current password, and receive the next password.

## Given Access

User: `bandit20`

Password:

```text
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

## Method

Start a local listener that sends the current password, then run `suconnect` against that port. When `suconnect` reads the expected password, it returns the next one.

## Commands

```bash
(printf "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO\n" | nc -l -p 45678) & sleep 1
./suconnect 45678
```

## Result

Program output:

```text
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

Password for `bandit21`:

```text
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

## Lesson

Some CTF services require controlling both ends of a connection. A one-shot `nc` listener is enough when the protocol is a single line in and a single line out.
