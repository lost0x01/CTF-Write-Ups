# Leviathan Level 04 to 05

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 4 -> 5 |
| Status | Complete |

## Objective

Recover the password for `leviathan5` from the hidden binary under `.trash/`.

## Given Access

User: `leviathan4`

Password:

```text
WG1egElCvO
```

## Recon

The home directory contains a hidden `.trash/` directory with a setuid binary named `bin`.

## Method

Running `.trash/bin` prints a sequence of binary octets:

```text
00110000 01100100 01111001 01111000 01010100 00110111 01000110 00110100 01010001 01000100 00001010
```

Convert each 8-bit chunk from binary to ASCII to recover the next password.

## Commands

```bash
ssh -p 2223 leviathan4@leviathan.labs.overthewire.org
.trash/bin
python3 - <<'EOF'
s='00110000 01100100 01111001 01111000 01010100 00110111 01000110 00110100 01010001 01000100 00001010'
print(''.join(chr(int(b,2)) for b in s.split()))
EOF
```

## Result

Password for `leviathan5`:

```text
0dyxT7F4QD
```

## Lesson

Not every challenge needs exploitation. Sometimes the right move is simply recognizing an encoding format and decoding it cleanly.

## References

- https://overthewire.org/wargames/leviathan/
