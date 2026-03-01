# 🔐 Cryptography Cheatsheet

## RSA Attacks
```python
# Small e (e=3)
import gmpy2
m, exact = gmpy2.iroot(ciphertext, 3)

# Common modulus
from sympy import gcdex
g, s, t = gcdex(e1, e2)
m = pow(c1,s,n) * pow(c2,t,n) % n
```

## XOR
```python
key = bytes(p ^ c for p, c in zip(plaintext, ciphertext))
def xor_key(data, key):
    return bytes(data[i] ^ key[i % len(key)] for i in range(len(data)))
```

## Hash ID
```
32  → MD5    40 → SHA1    64 → SHA256
128 → SHA512   60 → bcrypt ($2b$)
```

## Entropy
```python
import math
from collections import Counter
def entropy(d):
    c=Counter(d); t=len(d)
    return -sum((v/t)*math.log2(v/t) for v in c.values())
# >7.5 = likely encrypted
```
