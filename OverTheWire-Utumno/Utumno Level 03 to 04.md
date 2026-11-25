# Utumno Level 03 to 04

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Utumno |
| Level | 3 -> 4 |
| Status | In Progress / Blocked |

## Objective

Exploit the indexed byte-write logic in `utumno3` and recover the password for `utumno4`.

## Given Access

User: `utumno3`

Password:

```text
h3kVKJZuid
```

## Recon

Live disassembly showed this behavior:

1. `getchar()` reads one byte into `input`.
2. The program stores `input` into a local byte array at `buffer[i]` where `i` starts at `0`.
3. It then transforms that stored byte with:

```c
buffer[i] ^= (i * 3);
```

4. A second `getchar()` reads another byte.
5. That second byte is written to:

```c
*(ebp - 0x20 + transformed_index) = second_input;
```

6. The loop increments `i` and continues while `i <= 0x17` and input has not hit EOF.

Relevant layout from the function prologue:

- local workspace starts at `ebp-0x38`
- the second write targets memory relative to `ebp-0x20`
- there is no stack protector
- the program waits for stdin, so plain command-line execution hangs until input is provided

## Current Hypothesis

This looks like a two-byte-at-a-time arbitrary-ish stack write primitive:

- first byte controls the transformed index,
- second byte becomes the value written at `ebp-0x20 + transformed_index`.

Because the transformed index depends on the first byte and the current loop counter, the likely solve is to choose input pairs that steer writes onto saved EBP / saved EIP while preserving enough of the loop state to finish the overwrite.

## Verified Live Observations

Commands used:

```bash
ssh -p 2227 utumno3@utumno.labs.overthewire.org
objdump -d -M intel /utumno/utumno3 | sed -n '/<main>/,/^$/p'
timeout 2 /utumno/utumno3 test
```

Observed:

```text
RC:124
```

So the binary is definitely blocking on stdin rather than consuming argv.

## Next Continuation Point

The next practical step is to model the expression:

```text
transformed_index = (first_byte ^ (i * 3)) & 0xff
write_target      = ebp - 0x20 + transformed_index
```

and then choose per-iteration byte pairs that place controlled values over the saved frame or return address.

## Lesson

Even before a full solve, it is worth preserving the exact stack-relative write expression and loop bounds. With weird index-transformation challenges like this, those live details are the real continuation state.

## References

- https://overthewire.org/wargames/utumno/
