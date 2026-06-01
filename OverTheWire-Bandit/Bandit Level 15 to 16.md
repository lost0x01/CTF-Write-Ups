# Bandit Level 15 to 16

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 15 -> 16 |
| Status | Complete |

## Objective

Submit the current password to an SSL-enabled localhost service on port `30001`.

## Given Access

User: `bandit15`

Password:

```text
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

## Method

The service requires TLS, so `nc` is not enough. `openssl s_client` opens the encrypted connection and accepts the password through standard input.

## Commands

```bash
echo 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo | openssl s_client -quiet -connect localhost:30001
```

## Result

Service response:

```text
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

Password for `bandit16`:

```text
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

## Lesson

Use `openssl s_client` when a challenge service speaks TLS directly. Certificate warnings can be expected in lab services with self-signed certificates.
