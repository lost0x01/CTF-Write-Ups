# Natas Level 28 to 29

| Field | Value |
|---|---|
| Platform | OverTheWire |
| Wargame | Natas |
| Level | 28 -> 29 |
| Status | Complete |

## Objective

Exploit encrypted SQL execution through block alignment.

## Given Access

User: `natas28`

Password:

```text
1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj
```

## Method

The app encrypts the search query with block-cipher behavior that exposes a stable prefix. Ten bytes of padding align controlled SQL at a block boundary. Dropping the first three ciphertext blocks leaves an encrypted SQL statement that `search.php` decrypts and executes. A boolean SQL extractor recovered `SELECT password FROM users LIMIT 1`.

## Result

Password for `natas29`:

```text
31F4j3Qi2PnuhIZQokxXk1L3QT9Cppns
```

## Lesson

Encrypting a query is not a security boundary when the application later decrypts and executes attacker-controlled plaintext.

## References

- https://overthewire.org/wargames/natas/
