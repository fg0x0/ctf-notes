# 🔐 Cryptography Cheatsheet

## Shannon Entropy
```python
import math
from collections import Counter

def entropy(data: bytes) -> float:
    if not data: return 0
    c = Counter(data)
    t = len(data)
    return -sum((v/t)*math.log2(v/t) for v in c.values())

# Interpretation
# 0.0 – 3.0 → Repeating/padding
# 3.0 – 5.0 → Plaintext (JSON, HTML)
# 5.0 – 6.5 → Mixed (cookies, tokens)
# 6.5 – 8.0 → Encrypted / compressed
```

## RSA Attacks
```python
from Crypto.PublicKey import RSA

# Small e (e=3) — no padding
import gmpy2
c = int(ciphertext.hex(), 16)
m, exact = gmpy2.iroot(c, 3)
if exact:
    print(bytes.fromhex(hex(m)[2:]))

# Common modulus attack
# Given: c1 = m^e mod n, c2 = m^e mod n (same m, different e)
from math import gcd
from sympy import gcdex
g, s, t = gcdex(e1, e2)
m = pow(c1,s,n) * pow(c2,t,n) % n
```

## Hash Identification
```bash
hashid 'hash_here'
hash-identifier

# Common formats
32  chars  → MD5
40  chars  → SHA1
56  chars  → SHA224
64  chars  → SHA256
96  chars  → SHA384
128 chars  → SHA512
60  chars  → bcrypt ($2b$)
```

## XOR
```python
# Key recovery (known plaintext)
key = bytes(p ^ c for p, c in zip(plaintext, ciphertext))

# Repeating key XOR
def xor_key(data, key):
    return bytes(data[i] ^ key[i % len(key)] for i in range(len(data)))

# Key length detection — Kasiski / IoC
```

## Classic Ciphers
```python
# Caesar brute force
for shift in range(26):
    print(shift, ''.join(chr((ord(c)-65+shift)%26+65)
          if c.isalpha() else c for c in cipher.upper()))

# Vigenere decrypt
def vigenere_decrypt(cipher, key):
    return ''.join(
        chr((ord(c) - ord(k) - 65) % 26 + 65) if c.isalpha() else c
        for c, k in zip(cipher.upper(), (key*100).upper()))
```
