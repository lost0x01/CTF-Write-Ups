# Bandit Level 12 to 13

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 12 -> 13 |
| Status | Complete |

## Objective

Recover a password from a hex dump of a repeatedly compressed file.

## Given Access

User: `bandit12`

Password:

```text
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

## Method

Work in a temporary directory, reverse the hex dump with `xxd -r`, identify each archive/compression layer with `file`, rename as needed, and unpack repeatedly.

## Commands

```bash
tmp=$(mktemp -d)
cd "$tmp"
cp ~/data.txt .
xxd -r data.txt data.bin
file data.bin
mv data.bin data.gz
gzip -d data.gz
file data
mv data data.bz2
bzip2 -d data.bz2
file data
mv data data.gz
gzip -d data.gz
file data
tar xf data
file data5.bin
tar xf data5.bin
file data6.bin
mv data6.bin data6.bz2
bzip2 -d data6.bz2
file data6
tar xf data6
file data8.bin
mv data8.bin data8.gz
gzip -d data8.gz
file data8
cat data8
```

## Result

Password for `bandit13`:

```text
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

## Lesson

Use `file` after every extraction step. Archive chains are much easier when each layer is identified before acting.

