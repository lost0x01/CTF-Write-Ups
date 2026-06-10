# Narnia Level 04 to 05

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 4 -> 5 |
| Status | In Progress |

## Objective

Exploit the environment-scrubbing stack overflow in `narnia4` and recover `narnia5`.

## Given Access

User: `narnia4`

Password:

```text
iqNWNk173q
```

## Recon

`/narnia/narnia4.c` clears `environ[]` before copying `argv[1]` into a 256-byte stack buffer with `strcpy()`. That rules out the simple environment-shellcode technique from `narnia2` and pushes the exploit toward shellcode embedded directly in the overflowing argument.

## Progress So Far

- Verified the binary source and confirmed the environment wipe loop.
- Reproduced a crashing control-flow hijack attempt using an inline NOP sled, a setreuid+`/bin/sh` shellcode stub, and a candidate return target from a public write-up (`0xffffd510`).
- The current payload reaches the crash but has not yet yielded a stable privileged shell on this host, so the level remains unsolved in this session.

## References

- https://overthewire.org/wargames/narnia/
