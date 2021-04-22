# PhaseStream 3 and 4

## Challenge

### 3

```plain
The aliens have learned the stupidity of their misunderstanding of Kerckhoffs's principle.
Now they're going to use a well-known stream cipher (AES in CTR mode) with a strong key.
And they'll happily give us poor humans the source because they're so confident it's secure!
```

### 4

```plain
The aliens saw us break PhaseStream 3 and have proposed a quick fix to protect their new cipher.
```

## Solution

I was stumped by this one. I've never done much with `AES` and I know mostly nothing about it.

Sooo I started to try google a bit to see if there are any known weaknesses
within `AES CTR`. To make a long story short... Not really. The only thing I
found was an article about _crib_ attacks.

### crib attacks

A crib attacks can be done when the same keystream is used to encrypt to
different plaintexts! Well thats exactly what we have here.

The math behind it is quite fascinating and I want to give kudos to
[@FrankHassanabad][FrankHassanabad] who did did [a nice writeup about it][blog]

He also wrote a tool to do such an attack wich I shamelessly used here.

## Tooling

I wrote a small python script to xor the given cypertexts.

```python
with open('output.txt', 'r') as f:
    data = f.readlines()

data = [bytes.fromhex(elem) for elem in data]
# for j in range(len(data[0]) -len(data[1])):
test = bytes([data[0][i] ^ data[1][i] for i in range(len(data[1]))]).hex()
print(test)
```

This produced a mixed plaintext which can be attacked with a crib attack.

Here I used the tool from [@FrankHassanabad][FrankHassanabad] to do the crib
attack

## Attacking PhaseStream 3

Since a big example of the first plaintext was given the only thing I needed to
feed to the tool were the first words of the given plaintext

```plain
┌──(kali㉿kali)-[~/Desktop/phaseStream3/nodejs-cribdrag]
└─$ npm run cribdrag 0d27743012155b01155c027f1b41302955203114002413
? Please enter your crib: No right of private conversation
? Please enter your crib: No right of private conversa
? Please enter your crib: No right of private c
0: CHTB{r3u53d_k3Y_4TT4c
1: i|<ia|m;1B@#AEq G
2: :_2g2f}("}a@[<VP`ep
? Please enter your crib: No right of private con
0: CHTB{r3u53d_k3Y_4TT4cK}
```

## Attacking PhaseStream 4

This was a bit harder. The only plaintext I knew in this case was `CHTB{`

That was enough to get the following:

```bash
? Please enter your crib: CHTB{
0: I alo *** (possible drag match)
```

Well that seems to be the word `alone` so let's try that

```bash
? Please enter your crib: I alone #👈 note the space here since I was relatively sure a space followed after alone
0: CHTB{str
```

Hmm since we're doing stream cyphers the whole time lets try that

```bash
? Please enter your crib: CHTB{stream
0: I alone can *** (possible drag match)
```

Well now what... Let's try googling that - and would you look at that one of the
first quotes on google was from Mother Teresa:

```plain
I alone cannot change the world, but I can cast a stone across the waters to create many ripples
```

Since the Theme of the whole Hacking challenge is doing good and saving the
world this seemed plausible.

And it worked :-)

[FrankHassanabad]: https://github.com/FrankHassanabad
[blog]: https://medium.com/@fhbro/crib-dragging-plain-text-attack-5a61a0bcd80d
