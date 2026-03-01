# 🛠️ Tools Reference

## Recon
```bash
nmap -sV -sC -p- target
subfinder -d target.com
ffuf -u https://target/FUZZ -w wordlist.txt
```

## Web
```
Burp Suite, SQLmap, Nikto, Gobuster, WPScan
```

## Crypto
```
CyberChef — https://gchq.github.io/CyberChef
hashcat -m 0 hash.txt wordlist.txt
RsaCtfTool.py --publickey key.pem --uncipher cipher
```

## Pwn
```
pwntools, GDB+pwndbg, ROPgadget, one_gadget
```

## Forensics
```
binwalk, volatility3, wireshark, foremost, steghide, zsteg
```

## Wordlists
```
/usr/share/wordlists/rockyou.txt
/usr/share/seclists/
```
