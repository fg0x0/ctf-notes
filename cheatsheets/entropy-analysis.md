# Shannon Entropy Cheatsheet

## Entropy Values
| Range | Meaning | Example |
|-------|---------|---------|
| 0–3.0 | Very low — repeating | `aaaaaaaa`, padding |
| 3.0–5.0 | Low — plaintext | HTML, JSON |
| 5.0–6.5 | Medium — mixed | Cookies, tokens |
| 6.5–8.0 | High — encrypted/compressed | AES, gzip |

## Python One-liner
```python
import math; from collections import Counter
h = lambda d: -sum((c/len(d))*math.log2(c/len(d)) for c in Counter(d).values())
```

## Bug Bounty Signals
- Cookie entropy < 3.5 → Weak session token
- Auth token entropy < 4.0 → Predictable (SHA1/MD5)
- Response entropy > 7.5 without Content-Encoding → Suspicious
