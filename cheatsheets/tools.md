# 🛠️ CTF Tools Reference

## Recon & OSINT
```bash
nmap -sV -sC -p- target          # Full port scan
subfinder -d target.com           # Subdomain enum
httpx -l subdomains.txt           # Live host check
katana -u https://target.com      # Web crawler
ffuf -u https://target/FUZZ -w wordlist.txt   # Fuzzing
```

## Web
```
Burp Suite     → Intercept, Repeater, Intruder
SQLmap         → sqlmap -u "url" --dbs
Nikto          → nikto -h target
WPScan         → wpscan --url target (WordPress)
Gobuster       → gobuster dir -u url -w wordlist
```

## Crypto
```
CyberChef      → https://gchq.github.io/CyberChef
SageMath       → RSA, ECC math
hashcat        → hashcat -m 0 hash.txt wordlist.txt
john           → john --wordlist=rockyou.txt hash.txt
RsaCtfTool     → python RsaCtfTool.py --publickey key.pem --uncipher cipher
```

## Pwn
```
pwntools       → pip install pwntools
GDB + pwndbg   → git clone https://github.com/pwndbg/pwndbg
ROPgadget      → pip install ropgadget
ropper         → pip install ropper
one_gadget     → gem install one_gadget
```

## Forensics
```
binwalk        → apt install binwalk
volatility     → volatility3 -f mem.dmp windows.pslist
wireshark      → apt install wireshark
foremost       → apt install foremost
exiftool       → apt install libimage-exiftool-perl
steghide       → apt install steghide
zsteg          → gem install zsteg
```

## Wordlists
```bash
/usr/share/wordlists/rockyou.txt
/usr/share/seclists/                      # apt install seclists
https://github.com/danielmiessler/SecLists
```
