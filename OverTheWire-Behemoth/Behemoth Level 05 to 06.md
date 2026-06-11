# Behemoth Level 05 to 06

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Behemoth |
| Level | 5 -> 6 |
| Status | Complete |

## Objective

Capture the password that `behemoth5` exfiltrates over localhost UDP.

## Given Access

User: `behemoth5`

Password:

```text
mVfC4rBKZ4
```

## Recon

Strings/disassembly showed the binary opens `/etc/behemoth_pass/behemoth6`, resolves `localhost`, and uses UDP port `1337`.

## Method

Start a local UDP listener bound to `127.0.0.1:1337`, then execute `/behemoth/behemoth5`. The binary sends the next password over that socket.

## Commands

```bash
ssh -p 2221 behemoth5@behemoth.labs.overthewire.org
python3 - <<'PY'
import socket, subprocess, threading, time

def recv_once():
    s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    s.bind(('127.0.0.1', 1337))
    data, _ = s.recvfrom(4096)
    print(data.decode().strip())
    s.close()

t = threading.Thread(target=recv_once)
t.start()
time.sleep(0.5)
subprocess.run(['/behemoth/behemoth5'])
t.join()
PY
```

## Result

Password for `behemoth6`:

```text
j9I1wHzfVC
```

## Lesson

If a binary opens a socket after reading a protected file, assume it is trying to leak the secret and receive it yourself.

## References

- https://overthewire.org/wargames/behemoth/
