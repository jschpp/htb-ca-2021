# Nintendo Base64

Man erhält folgendes Ascii Art als Hinweis.
Besonderes Augenmerk sollte auf der (x8) liegen^^.

Außerdem ist der Titel der Chanllenge ein weiterer Hinweis.

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

Wenn man obigen Text von whitespace bereinigt und __8__ mal Base64 decodiert erhält man die Flag

```python
import base64
with open("output.txt", "r") as f:
    data = f.read()

result = data.replace(" ", "").replace("\n","")
for i in range(8):
    result = base64.b64decode(result).decode('ascii')

print(result)
```
