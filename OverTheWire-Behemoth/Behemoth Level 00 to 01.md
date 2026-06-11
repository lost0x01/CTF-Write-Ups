# Behemoth Level 00 to 01

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Behemoth |
| Level | 0 -> 1 |
| Status | Complete |

## Objective

Recover the password check input for `behemoth0` and use it to reach `behemoth1`.

## Given Access

User: `behemoth0`

Password:

```text
behemoth0
```

## Recon

The binary does not print the compared password directly, but reversing/ltrace quickly shows the transformed check value. The required input is the decoded memfrob-style string.

## Method

Trace the comparison, recover the cleartext password `eatmyshorts`, then run the binary with that input and read the next password file from the spawned shell.

## Commands

```bash
ssh -p 2221 behemoth0@behemoth.labs.overthewire.org
ltrace /behemoth/behemoth0
/behemoth/behemoth0
# enter: eatmyshorts
whoami
cat /etc/behemoth_pass/behemoth1
```

## Result

Password for `behemoth1`:

```text
8YpAQCAuKf
```

## Lesson

Even the first Behemoth level rewards basic tracing before deeper reversing.

## References

- https://overthewire.org/wargames/behemoth/
