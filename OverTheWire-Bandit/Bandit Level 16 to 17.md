# Bandit Level 16 to 17

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 16 -> 17 |
| Status | Complete |

## Objective

Find the correct localhost service between ports `31000` and `32000`, submit the current password, and recover an SSH private key for `bandit17`.

## Given Access

User: `bandit16`

Password:

```text
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

## Method

Scan the port range for open services, then test the open ports with `openssl s_client`. The useful service is the SSL endpoint that returns an SSH private key after receiving the correct password.

## Commands

```bash
nmap -p31000-32000 --open localhost
```

Open ports:

```text
31046/tcp
31518/tcp
31691/tcp
31790/tcp
31960/tcp
```

Test each open port:

```bash
printf "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx\n" | timeout 5 openssl s_client -quiet -connect localhost:31790 2>/dev/null
```

The returned private key was saved locally as:

```text
05 Security Research/CTF/Over The Wire/Bandit/Artifacts/bandit17_sshkey.private
```

## Result

The service on port `31790` returned a private key for `bandit17`.

## Lesson

Port discovery and service validation are separate steps. First identify what is open, then interact with each candidate using the protocol the challenge expects.
