# PhaseStream 2

## Challenge

```plain
The aliens have learned of a new concept called "security by obscurity".
Fortunately for us they think it is a great idea and not a description of a common mistake.
We've intercepted some alien comms and think they are XORing flags with a single-byte key
and hiding the result inside 9999 lines of random data, Can you find the flag?
```

## Solution

I used a simple brute-force algorithm here:

```python
with open('output.txt', 'r') as f:
    for line in f:
        b = bytes.fromhex(line)
        for i in range(255):
            if chr(b[0] ^ i) == 'C':
                t = "".join([chr(j ^ i) for j in b])
                if t.isascii():
                    print(t)
```
