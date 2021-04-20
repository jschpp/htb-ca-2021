# PhaseStream 1

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
