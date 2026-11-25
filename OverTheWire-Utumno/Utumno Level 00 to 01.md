# Utumno Level 00 to 01

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Utumno |
| Level | 0 -> 1 |
| Status | Complete |

## Objective

Recover the password embedded inside the execute-only binary `utumno0`.

## Given Access

User: `utumno0`

Password:

```text
utumno0
```

## Recon

`/utumno/utumno0` was executable but not readable, so direct `strings`, `objdump`, `gdb`, and `ltrace` against the file path were not enough to recover its contents. Running it only printed:

```text
Read me! :P
```

Because the binary was not setuid, `LD_PRELOAD` still applied. That made it possible to hook `puts()` and dump the in-memory image after the executable had already been mapped by the loader.

## Method

1. Build a 32-bit shared object that overrides `puts()`.
2. Inside the hook, dump the mapped text/data region starting at `0x08048000` to `/tmp/u0_dump.bin`.
3. Also scan that same region for printable strings and save them to `/tmp/u0_strings.txt`.
4. Run `/utumno/utumno0` with `LD_PRELOAD=/tmp/hookputs.so`.
5. Read the dumped strings and recover the next password.

## Commands

```bash
ssh -p 2227 utumno0@utumno.labs.overthewire.org
cd /tmp
cat > hookputs.c <<'EOF'
#define _GNU_SOURCE
#include <dlfcn.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>
#include <ctype.h>

static int dumped = 0;

int puts(const char *s) {
    static int (*real_puts)(const char *) = NULL;
    if (!real_puts) real_puts = dlsym(RTLD_NEXT, "puts");
    if (!dumped) {
        dumped = 1;
        int fd = open("/tmp/u0_dump.bin", O_CREAT|O_WRONLY|O_TRUNC, 0644);
        if (fd >= 0) {
            write(fd, (void*)0x08048000, 0x4000);
            close(fd);
        }
        int out = open("/tmp/u0_strings.txt", O_CREAT|O_WRONLY|O_TRUNC, 0644);
        if (out >= 0) {
            unsigned char *p = (unsigned char*)0x08048000;
            unsigned char *end = (unsigned char*)0x0804c000;
            while (p < end) {
                if (isprint(*p)) {
                    unsigned char *q = p;
                    while (q < end && isprint(*q)) q++;
                    if (q - p >= 4) {
                        write(out, p, q - p);
                        write(out, "
", 1);
                    }
                    p = q;
                } else {
                    p++;
                }
            }
            close(out);
        }
    }
    return real_puts(s);
}
EOF
TMPDIR=/tmp gcc -m32 -fPIC -shared -o /tmp/hookputs.so /tmp/hookputs.c -ldl
LD_PRELOAD=/tmp/hookputs.so /utumno/utumno0
head -n 20 /tmp/u0_strings.txt
```

## Result

The dumped string list included:

```text
password: ytvWa6DzmL
```

That password was then verified by logging in directly as `utumno1`.

## Lesson

Execute-only binaries are still fair game when they are not setuid and can be coerced into loading attacker-controlled helper libraries. Dumping the mapped image at runtime is often simpler than trying to reconstruct it via ptrace.

## References

- https://overthewire.org/wargames/utumno/
