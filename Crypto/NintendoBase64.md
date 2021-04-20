# Nintendo Base64

## Challenge

```plain
Aliens are trying to cause great misery for the human race by using our own cryptographic technology to encrypt all our games.
Fortunately, the aliens haven't played CryptoHack so they're making several noob mistakes.
Therefore they've given us a chance to recover our games and find their flags.
They've tried to scramble data on an N64 but don't seem to understand that encoding and ASCII art are not valid types of encryption!
```

## Solution

The challenge consists of the ascii art below.
A very important part of the art is the times 8 (x8) in it!

Futhermore the challenge title is a very important part of the challenge itself
since it tells us to consider using `base64` encoding.

```plain
            Vm                                                   0w               eE5GbFdWW         GhT            V0d4VVYwZ
            G9              XV                                   mx              yWk    ZOV       1JteD           BaV     WRH
                            YW                                   xa             c1              NsWl dS   M1   JQ WV       d4
S2RHVkljRm  Rp UjJoMlZrZH plRmRHV m5WaVJtUl hUVEZLZVZk   V1VrZFpWMU  pHVDFaV1Z  tSkdXazlXYW   twdl   Yx    Wm Fj  bHBFVWxWTlZ
Xdz     BWa 2M xVT     FSc  1d   uTl     hi R2h     XWW taS     1dG VXh     XbU ZTT     VdS elYy     cz     FWM    kY2VmtwV2
JU       RX dZ ak       Zr  U0   ZOc2JGWmlS a3       BY V1       d0 YV       lV MH       hj RVpYYlVaVFRWW  mF lV  mt       3V
lR       GV 01 ER       kh  Zak  5rVj   JFe VR       Ya Fdha   3BIV mpGU   2NtR kdX     bWx          oT   TB   KW VYxW   lNSM
Wx       XW kV kV       mJ  GWlRZ bXMxY2xWc 1V       sZ  FRiR1J5VjJ  0a1YySkdj   RVpWVmxKV           1V            GRTlQUT09
```

After removing the whitespace and decoding the above __8__ times with `base64`
you receive the flag.

```python
import base64
with open("output.txt", "r") as f:
    data = f.read()

result = data.replace(" ", "").replace("\n","")
for i in range(8):
    result = base64.b64decode(result).decode('ascii')

print(result)
```
