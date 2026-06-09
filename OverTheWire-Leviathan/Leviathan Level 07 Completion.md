# Leviathan Level 07 Completion

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 7 |
| Status | Complete |

## Objective

Confirm completion of the Leviathan wargame.

## Given Access

User: `leviathan7`

Password:

```text
qEs5Io5yM8
```

## Method

Log in as `leviathan7` and read the completion file in the home directory.

## Commands

```bash
ssh -p 2223 leviathan7@leviathan.labs.overthewire.org
ls -la
cat CONGRATULATIONS
```

## Result

```text
Well Done, you seem to have used a *nix system before, now try something more serious.
(Please don't post writeups, solutions or spoilers about the games on the web. Thank you!)
```

## Lesson

Leviathan is complete after successfully reaching `leviathan7` and reading the completion message.

## References

- https://overthewire.org/wargames/leviathan/
