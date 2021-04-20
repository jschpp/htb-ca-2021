# PhaseStream 1

## Challenge

```plain
The aliens are trying to build a secure cipher to encrypt all our games called "PhaseStream". They've heard that stream ciphers are pretty good. The aliens have learned of the XOR operation which is used to encrypt a plaintext with a key. They believe that XOR using a repeated 5-byte key is enough to build a strong stream cipher. Such silly aliens! Here's a flag they encrypted this way earlier. Can you decrypt it (hint: what's the flag format?) 2e313f2702184c5a0b1e321205550e03261b094d5c171f56011904
```

## Solution

```python
s = r"2e313f2702184c5a0b1e321205550e03261b094d5c171f56011904"
arr = bytearray.fromhex(s)
KnownPlaintext = "CHTB{"
KeySize = 5
chunks = [arr[i:i+KeySize] for i in range(0, len(arr), KeySize)]

# Find key
key = ""
for i in range(5):
    key += chr(chunks[0][i] ^ ord(KnownPlaintext[i]))

# Decrypt cyphertext
result=""
for chunk in chunks:
    for i in range(5):
        if(i < len(chunk)):
            result += chr(chunk[i] ^ ord(key[i]))

print(result)
```
