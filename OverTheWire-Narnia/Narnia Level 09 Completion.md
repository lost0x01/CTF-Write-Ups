# Narnia Level 09 Completion

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 9 |
| Status | Complete |

## Objective

Confirm completion of the Narnia wargame.

## Given Access

User: `narnia9`

Password:

```text
1FFD4HnU4K
```

## Method

Log in as `narnia9` and read the completion file in the home directory.

## Commands

```bash
ssh -p 2226 narnia9@narnia.labs.overthewire.org
cat ~/CONGRATULATIONS
```

## Result

```text
you are l33t! next plz...

(Please don't post writeups, solutions or spoilers about the games on the web. Thank you!)
```

## Lesson

Narnia is complete after reaching `narnia9`, verifying the password with a direct login, and reading the final completion message.

## References

- https://overthewire.org/wargames/narnia/
